using Mono.Cecil;
using Mono.Cecil.Cil;
using System.Linq;

var assembly = AssemblyDefinition.ReadAssembly("your.dll");

foreach (var type in assembly.MainModule.Types)
{
    foreach (var method in type.Methods)
    {
        if (!method.HasBody) continue;

        foreach (var instruction in method.Body.Instructions)
        {
            // new O... class
            if (instruction.OpCode == OpCodes.Newobj)
            {
                var methodRef = instruction.Operand as MethodReference;
                var declaringType = methodRef.DeclaringType;

                if (declaringType.Name.StartsWith("O"))
                {
                    Console.WriteLine($"New instance: {declaringType.FullName}");
                }
            }

            // method çağrısı
            if (instruction.OpCode == OpCodes.Call || 
                instruction.OpCode == OpCodes.Callvirt)
            {
                var calledMethod = instruction.Operand as MethodReference;

                if (calledMethod.DeclaringType.Name.StartsWith("O"))
                {
                    Console.WriteLine(
                        $"Call: {calledMethod.DeclaringType.Name}.{calledMethod.Name}");
                }
            }
        }
    }
}
