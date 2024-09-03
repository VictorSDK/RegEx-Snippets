# RegEx-Snippets
Useful RegEx snippets for tedious coding tasks

## Snippets

### C#

***Replace Full properties with auto-properties***
```
public (\w+) (\w+)\r\n +\{\r\n +get\r\n +\{\r\n +return this.*;\r\n +\}\r\n +set\r\n +\{\r\n +this.*;\r\n +\}\r\n +\}\r\n
public $1 $2 { get; set; }
```

***Remove private variables***
```
private \w+ \w+Field;\r\n\r\n
```

***Auto properties to constructor assignments***
```
public \w+\?? (\w+) \{ get; set; \}
$1$2 = \l$1$2;
```

***Auto properties to parameters***
```
public (\w+\??) (\w+) \{ get; set; \}
$1 \l$2 = null,
```

***Auto properties to assign properties only if have value***
strings
```
public string (\w+) \{ get; set; \}
if \(!string.IsNullOrWhiteSpace\(reportLine.$1\)\) reporLineDao.$1 = reportLine.$1;
```
nullables
```
public \w+\?? (\w+) \{ get; set; \}
if \(reportLine.$1.HasValue\) reporLineDao.$1 = reportLine.$1;
```

***Auto properties to assign if not null or empty***
strings
```
public string (\w+) \{ get; set; \}
if \(\($1 \?\? ""\).Trim\(\)  != \(other.$1\ ?\? ""\).Trim\(\)\) return false;
```
objects
```
public \w+\?? (\w+) \{ get; set; \}
if \($1  != other.$1\) return false;
```

***CSV to sb.Append***
```
(\w+[\s\w]*,)
sb.Append\("$1"\);\n\r
```

***Column name to AutoProperties with CsvFileReader Attributes***
```
(\w+)
[Name\("$1"\)]\r\npublic string \u$1 { get; set; }\r\n
```

### C# To JSON
***Auto properties to JSON schema properties***
```
public \w+\?? (\w+) \{ get; set; \}
"\l$1": \{\r\n\t"type":"number"\r\n\},\r\n
```

***Auto properties to JSON***
```
public \w+\?? (\w+) \{ get; set; \}
"\l$1": ,\r\n
```


### JSON To C#
***JSON properties to C# assignments***
```
\"(\w+)\": (.*),
\u$1 = $2,
```

***JSON properties to C# JObject assignments***
properties
```
\"(\w+)\": (.*)
\[\"$1\"\] = $2
```
elements
```
\"(\w+)\": \{
\[\"$1\"\] = new JObject \{
```

***JSON to C# property***
```
\“(\w+)\”: (.*),?
public string \u$1 { get; set; }
```

***JSON to something else***
```
\“(\w+)\”: (.*),
\l$1: $2,
```

### TypeScript

***Typescript enum to Jest test***
```
(\w{2}) = ('.+'),?
expect\(fixture.find\('.vi label[htmlFor="$1"]'\).text\(\)\).toBe\($2\)\r\nexpect\(fixture.find\('.vi label[htmlFor="$1"] input'\).props\(\).checked\).toBeFalsy\(\)
```

### Cypress

***Cypress to JSON camelcase***
```
(\w+): (.*),?
\"\l$1\": $2,
```
