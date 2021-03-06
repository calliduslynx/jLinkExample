## Java Version mind. 11
`java --version`


## compile
```
javac -d out src/module-info.java
javac -d out --module-path out src/de/mabe/project/P1.java
```

## starten
`java --module-path out --module ppp/de.mabe.project.P1`

## Abhängigkeiten anzeigen
`jdeps --module-path out -s --module ppp`



## JRE bauen
`jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --output jre`

... bissel kleiner (nicht mal ein MB)

`jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre`

... mit compress (ca. 50% weniger) ... https://stackoverflow.com/a/55716907

| 0=aus | 1=Constant String Sharing | 2=ZIP | Hinweis |
|-------|---------------------------|-------|---------|
| 40MB  |   33MB                    | 27MB  ||
| 14MB  |   13MB                    | 15MB  | <-- wenn danach alles gezippt|
| 34MB  |   28MB                    | 25MB  ||
| 11MB  |   11MB                    | 13MB  | <-- wenn danach alles gezippt|

```
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre0 --compress=0
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre1 --compress=1
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre2 --compress=2
```

```
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre0s --compress=0 --strip-debug
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre1s --compress=1 --strip-debug
jlink --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --no-header-files --no-man-pages --output jre2s --compress=2 --strip-debug
```


Ideal: mit ```--compress=1 --strip-debug```



## JRE starten
```jre/bin/java --module ppp/de.mabe.project.P1```

## JRE Module anzeigen
```jre/bin/java --list-modules```


## JRE inkl. Launcher bauen
```jlink --launcher start_ppp=ppp/de.mabe.project.P1 --module-path "out:/Users/calliduslynx/.jenv/versions/11.0.5/jmods"  --add-modules ppp --output jre --compress=2```

... start_ppp ist Name der Datei

... starten mit
```jre/bin/start_ppp```