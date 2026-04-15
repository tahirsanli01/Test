using Mono.Cecil;
using Mono.Cecil.Cil;
using System.Collections.Generic;
using System.Linq;
using System.Text.Json;

public static class DllAnalyzer
{
    public static string GetClassMethodMapAsJson(string dllPath)
    {
        var result = new Dictionary<string, Dictionary<string, MethodDetail>>();

        var assembly = AssemblyDefinition.ReadAssembly(dllPath);

        foreach (var type in assembly.MainModule.Types)
        {
            foreach (var method in type.Methods)
            {
                if (!method.HasBody)
                    continue;

                foreach (var instruction in method.Body.Instructions)
                {
                    if (instruction.OpCode == OpCodes.Call ||
                        instruction.OpCode == OpCodes.Callvirt)
                    {
                        var called = instruction.Operand as MethodReference;
                        if (called == null)
                            continue;

                        var className = called.DeclaringType.Name;

                        // filtre
                        if (!className.StartsWith("O"))
                            continue;

                        if (!result.ContainsKey(className))
                            result[className] = new Dictionary<string, MethodDetail>();

                        var methodName = called.Name;

                        if (!result[className].ContainsKey(methodName))
                        {
                            var parameters = called.Parameters
                                .Select(p => $"{p.ParameterType.Name} {p.Name}")
                                .ToList();

                            var returnType = called.ReturnType.Name;

                            result[className][methodName] = new MethodDetail
                            {
                                Method = methodName,
                                Parameters = parameters,
                                ReturnType = returnType
                            };
                        }
                    }
                }
            }
        }

        // JSON serialize
        var options = new JsonSerializerOptions
        {
            WriteIndented = true
        };

        return JsonSerializer.Serialize(result, options);
    }
}

public class MethodDetail
{
    public string Method { get; set; }
    public List<string> Parameters { get; set; }
    public string ReturnType { get; set; }
}
