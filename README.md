# ilivalidator-native

Native Images von _ilivalidator_ für Windows, macOS und Linux. Java wird nicht mehr benötigt. Die grafische Oberfläche wird nicht unterstützt.

```
./ilivalidator --help
```

Für jede Version von _ilivalidator_ gibt es einen Branch, z.B. `V_1_12_1`. Das Native Image wird als Zip-Datei unter https://github.com/edigonzales/ili2pg-native/releases veröffentlicht. Die Zahl nach dem Unterstrich entspricht der Buildnummer der Github-Action. Der main-Branch kann keine Releases machen.

Plugin-Unterstützung funktioniert nicht. Sie müssten vorgängig reinkompiliert werden.

## Develop

Die GraalVM-Konfig-Dateien müssen nicht mit dem Agent hergestellt werden. Interessanterweise "schlüpft" mit dem Agent eine GUI-Klasse rein, die dann beim Ausführen des Programmes zum Absturz führt:

```
java -agentlib:native-image-agent=config-output-dir=conf-dir -jar /Users/stefan/apps/ilivalidator-1.12.1/ilivalidator-1.12.1.jar --allObjectsAccessible /Users/stefan/Downloads/ch.so.arp.bauzonengrenzen_xtf/ch.so.arp.bauzonengrenzen.xtf
```

Problem-Klasse (die entfernt werden muss)

```
{
  "name":"org.interlis2.validator.gui.MainFrame",
  "methods":[{"name":"main","parameterTypes":["java.lang.String[]","ch.ehi.basics.settings.Settings"] }]
}
```

Müsste analysiert werden, warum die Klasse mit dem Agent gefunden wird.