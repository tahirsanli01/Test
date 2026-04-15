using Mono.Cecil;
using Mono.Cecil.Cil;
using System;
using System.Collections.Generic;
using System.Linq;

var assembly = AssemblyDefinition.ReadAssembly("test.dll");

// sonuç: Class -> Method listesi
var result = new Dictionary<string, HashSet<string>>();

foreach (var type in assembly.MainModule.Types)
{
    foreach (var method in type.Methods)
    {
        if (!method.HasBody) continue;

        foreach (var instruction in method.Body.Instructions)
        {
            if (instruction.OpCode == OpCodes.Call ||
                instruction.OpCode == OpCodes.Callvirt)
            {
                var called = instruction.Operand as MethodReference;
                if (called == null) continue;

                var className = called.DeclaringType.Name;

                // filtre (O ile başlayanlar)
                if (!className.StartsWith("O"))
                    continue;

                if (!result.ContainsKey(className))
                    result[className] = new HashSet<string>();

                result[className].Add(called.Name);
            }
        }
    }
}
