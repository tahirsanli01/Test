using Mono.Cecil;
using Mono.Cecil.Cil;
using System.Collections.Generic;

public static class DllAnalyzer
{
    public static Dictionary<string, List<string>> GetClassMethodMap(string dllPath)
    {
        var result = new Dictionary<string, HashSet<string>>();

        var assembly = AssemblyDefinition.ReadAssembly(dllPath);

        foreach (var type in assembly.MainModule.Types)
        {
            foreach (var method in type.Methods)
            {
                // Body yoksa geç
                if (!method.HasBody)
                    continue;

                foreach (var instruction in method.Body.Instructions)
                {
                    // Method çağrısı yakala
                    if (instruction.OpCode == OpCodes.Call ||
                        instruction.OpCode == OpCodes.Callvirt)
                    {
                        var called = instruction.Operand as MethodReference;
                        if (called == null)
                            continue;

                        var className = called.DeclaringType.Name;

                        // Sadece O ile başlayan classlar
                        if (!className.StartsWith("O"))
                            continue;

                        if (!result.ContainsKey(className))
                            result[className] = new HashSet<string>();

                        result[className].Add(called.Name);
                    }
                }
            }
        }

        // HashSet → List dönüşümü
        var finalResult = new Dictionary<string, List<string>>();

        foreach (var item in result)
        {
            finalResult[item.Key] = new List<string>(item.Value);
        }

        return finalResult;
    }
}
