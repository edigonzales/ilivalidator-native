# ilivalidator-native

## Todo

- Tests
- Plugins? Werden nicht so funktionieren können, muss man reinkompilieren. Siehe z.B. ilivalidator web service.


## Native image agent

```
java -agentlib:native-image-agent=config-output-dir=conf-dir -jar /Users/stefan/Downloads/ilivalidator-1.12.0/ilivalidator-1.12.0.jar --allObjectsAccessible /Users/stefan/Downloads/ch.so.arp.bauzonengrenzen_xtf/ch.so.arp.bauzonengrenzen.xtf
```

Die Gui-Klassen aus _reflect-config.json_ entfernen:

```
{
  "name":"org.interlis2.validator.gui.MainFrame",
  "methods":[{"name":"main","parameterTypes":["java.lang.String[]","ch.ehi.basics.settings.Settings"] }]
}
```
Mir ist nicht ganz klar, warum die jetzt reinrutschen. Wobei der Agent glaub beim ilivalidator nicht notwendig wäre. Dann passiert das auch nicht. Zeigt, dass das ganze Gui-Zeugs nocht nicht befriedigend mit native image funktioniert (bei GraalVM sowieso nicht, bei Liberica NIK bissle besser). Und auch UX/UI keine Zukunft hat (meine Meinung). Ich weiss nicht, ob die Code-Lösung im ilivalidator eher ein - sorry - "Schlaumeierei" ist, oder ob diese native-image-Kompatibilität state-of-the art ist. Tendenz eher i.O., da die AWT-Klasse vom Agent wegen den Settings gefunden wird?