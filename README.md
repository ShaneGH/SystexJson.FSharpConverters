# SystexJson.FSharpConverters
JsonConverters and Factories for FSharp types in System.Text.Json

Serializes/Deserializes

* Discriminated Unions
* Options
* Tuples
* Record Types
* Lists

## Install

You can

1. Just copy paste the source code: https://github.com/ShaneGH/SystexJson.FSharpConverters/blob/master/SystexJson.FSharpConverters/FSharpConverters.fs
1. Get the Nuget package: `dotnet add package SystexJson.FSharpConverters`

## Use

```F#
open SystexJson.FSharpConverters
open System.Text.Json

type ExampleType =
    {
        Value: string option
    }

let options =
    let opt = JsonSerializerOptions()
    
    Factories.Build()
    |> List.map opt.Converters.Add
    |> (fun _ -> opt)
    
let value = { Value = Some "Hi" }
    
let json = JsonSerializer.Serialize (value, options)
let valueAfter = JsonSerializer.Deserialize<ExampleType> (json, options)
```