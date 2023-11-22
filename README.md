# Programmierung eines Python-Algorithmus zur automatischen Aktualisierung einer Datei

## Projektbeschreibung

In diesem Projekt geht es darum, den Zugriff auf zugangsbeschränkte Inhalte anhand einer Textdatei mit einer Liste von IP-Adressen zu kontrollieren. Die Textdatei `'allow_list.txt'` enthält die Allow-Liste mit den IP-Adressen, die auf die zugangsbeschränkten Inhalte zugreifen dürfen. In einer separaten Remove-Liste sind die IP-Adressen aufgeführt, die keinen Zugriff mehr auf diese Inhalte haben und deshalb von der Allow-Liste entfernt werden sollen. Nachfolgend habe ich einen Algorithmus in Python programmiert, der die Datei `'allow_list.txt'` automatisch aktualisiert, indem er die IP-Adressen von der Allow-Liste entfernt, die keine Zugriffsberechtigung mehr haben.

## Die Datei mit der Allow-Liste öffnen

Als erstes habe ich den Namen der Textdatei, `'allow_list.txt'`, als String der Variablen `import_file` zugewiesen. Die Textdatei enthält die Allow-Liste mit den IP-Adressen, die Zugriff auf die zugangsbeschränkten Inhalte erhalten sollen. Als zweites habe ich die Remove-Liste mit den IP-Adressen, die von der Allow-Liste entfernt werden sollen, der Variablen `remove_list` zugewiesen.

```Python
# Weise den Dateinamen `import_list.txt` der Variablen import_file zu.

import_file = 'allow_list.txt'

# Weise die Liste mit den IP-Adressen, die von der Allow-Liste entfernt werden sollen, der Variablen `remove_list` zu.

remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]
```

Als nächstes habe ich eine `with` Anweisung verwendet, um die Datei zu öffnen:

```Python
# Erstelle eine `with` Anweisung, um den Inhalt der Datei einzulesen.

with open(import_file, 'r') as file:
```

Der Algorithmus verwendet den Code `with open(import_file, 'r') as file:`, um die Textdatei `'allow_list.txt'` zu öffnen. Die `with` Anweisung hilft bei der Verwaltung der Systemressourcen, indem es die Datei nach Beendigung der `with` Anweisung wieder schließt. Die `open()` Funktion hat zwei Parameter. Der erste Parameter, `import_file`, gibt die zu importierende Datei an. Der zweite Parameter, `'r'`, gibt an, dass auf die Datei im Lesemodus zugegriffen wird. Das `as` Schlüsselwort gibt die Anweisung, dass die Ausgabe der `open()` Funktion, in diesem Fall die Allow-Liste mit den IP-Adressen, in einer Variable namens `file` gespeichert wird.

## Den Inhalt der Datei lesen

Um den Inhalt der Datei zu lesen, verwendet der Algorithmus die `.read()` Methode, um ihn in einen String umzuwandeln.

```Python
with open(import_file, 'r') as file:

	# Verwende die `.read()` Methode, um den Inhalt der importierten Datei zu lesen, und weise ihn der Variable `ip_addresses` zu.
	
	ip_addresses = file.read()

# Gib den Inhalt der Allow-Liste aus.

print(ip_addresses)
```

Da die `open()` Funktion den Parameter `'r'` für den Lesemodus enthält, kann die `.read()` Methode innerhalb der `with` Anweisung verwendet werden. Die `.read()` Methode wandelt den Inhalt einer Datei in einen String um und ermöglicht es, ihn auf diese Weise zu lesen. In diesem Fall wird die `.read()` Methode auf die in der `with` Anweisung angegebene Variable, hier die Variable `file`, angewendet. Anschließend wird der ausgegebene String einer Variablen namens `ip_addresses` zugewiesen. Die `print()` Funktion gibt den aktuellen Inhalt der Allow-Liste aus.

## Den String in eine Liste umwandeln

Damit einzelne IP-Adressen aus der Allow-Liste entfernt werden können, muss sie im Listenformat vorliegen. Daher verwendet der Algorithmus die `.split()` Methode, die den in der Variablen `ip_addresses` enthaltenen String in eine Liste umwandelt:

```Python
# Verwende die `.split()` Methode, um den String `ip_addresses` in eine Liste umzuwandeln.

ip_addresses = ip_addresses.split()
```

Die `.split()` Methode wird aufgerufen, indem sie an eine String-Variable angehängt wird. Sie wandelt den Inhalt eines Strings in eine Liste um. Standardmäßig teilt die `.split()` Methode einen String anhand eines Trennzeichens in einzelne Listenelemente. In diesem Algorithmus nimmt die `.split()` Methode die in der Variablen `ip_addresses` gespeicherten Daten, in diesem Fall eine Zeichenfolge von IP-Adressen, die jeweils durch ein Leerzeichen getrennt sind, und wandelt diese Zeichenfolge in eine Liste von IP-Adressen um. Um diese Liste zu speichern, wird sie wieder der Variablen `ip_addresses` zugewiesen.

## Die Remove-Liste wiederholt durchlaufen

Ein wichtiger Bestandteil des Algorithmus besteht darin, die IP-Adressen zu durchlaufen, die auf der Liste `remove_list` stehen. Zu diesem Zweck habe ich eine `for` Schleife eingebaut:

```Python
# Erstelle eine `for` Schleife,
# nenne die Schleifenvariable `element`
# und durchlaufe die Liste 'remove_list'.

for element in remove_list:
```

Die `for` Schleife in Python wiederholt den Code für eine bestimmte Sequenz. Der allgemeine Zweck der `for` Schleife in einem Python-Algorithmus wie diesem besteht darin, bestimmte Code-Anweisungen auf alle Elemente einer Sequenz anzuwenden. Das Schlüsselwort `for` leitet die `for` Schleife ein. Es folgt die Schleifenvariable `element` und das Schlüsselwort `in`. Das Schlüsselwort `in` gibt an, dass der Algorithmus die Sequenz `ip_addresses` durchläuft und jeden Wert der Schleifenvariable `element` zuweist.

## IP-Adressen entfernen, die auf der Remove-Liste stehen

Der Algorithmus entfernt jede IP-Adresse aus der Allow-Liste `ip_addresses`, die in der Remove-Liste `remove_list` enthalten sind. Da es in `ip_addresses` keine Duplikate gibt, kann der folgende Code dafür verwendet werden:

```Python
for element in remove_list:

	# Erstelle eine `if` Bedingung, um zu prüfen, ob `element` in `ip_addresses` enthalten ist.

	if element in ip_addresses:

		# Verwende die `.remove()` Methode, um Elemente von der Liste `ip_addresses` zu entfernen.

		ip_addresses.remove(element)
```

Zunächst überprüft eine `if` Bedingung innerhalb der `for` Schleife, ob die Schleifenvariable `element` in der Allow-Liste `ip_addresses` enthalten ist. Diese Überprüfung ist erforderlich, da die Anwendung der `.remove()` Methode auf Elemente, die nicht in `ip_addresses` enthalten sind, sonst zu einem Fehler führen würde.

In dem Code-Abschnitt `ip_addresses.remove(element)` wird dann die `.remove()` Methode auf `ip_addresses` angewendet. Die Schleifenvariable `element` wird als Argument übergeben, so dass jede IP-Adresse, die in der Remove-Liste `remove_list` enthalten ist, aus der Allow-Liste `ip_addresses` entfernt wird.

## Die Datei mit der überarbeiteten Liste der IP-Adressen aktualisieren

Im letzten Schritt aktualisiert der Algorithmus die Textdatei `'allow_list.txt'` mit der überarbeiteten Liste der IP-Adressen. Dazu muss die Allow-Liste `ip_addresses` zunächst wieder in einen String umgewandelt werden. Hierfür verwendet der Algorithmus die `.join()` Methode:

```Python
# Wandel die Allow-Liste `ip_addresses` wieder in einen String um, damit es in die Textdatei geschrieben werden kann.

ip_addresses = '\n'.join(ip_addresses)
```

In Python kombiniert die `.join()` Methode alle Elemente in einer Liste zu einem String. In diesem Fall verwendet der Algorithmus die `.join()` Methode, um einen String aus der Allow-Liste `ip_addresses` zu erstellen. Die Zeichenfolge `('\n')` stellt das Trennzeichen dar und weist Python an, jedes Element innerhalb des Strings in eine neue Zeile zu schreiben.

Im nächsten Schritt wird `ip_addresses` als Argument an die `.write()` Methode übergeben. Die `.write()` Methode überschreibt dann den vorhandenen Inhalt der Textdatei `'allow_list.txt'` mit der überarbeiteten Allow-Liste `ip_addresses` im String-Format:

```Python
# Erstelle eine `with` Anweisung, um die Textdatei zu aktualisieren.

with open(import_file, 'w') as file:

	# Überschreibe den Inhalt der Textdatei mit der aktualisierten Liste `ip_addresses`.

	file.write(ip_addresses)
```

In dem Code-Abschnitt `with open(import_file, 'w') as file:` werden in der `with` Anweisung zwei Parameter an die `open()` Funktion übergeben: der erste Parameter `import_file` verweist auf die Textdatei `'allow_list.txt'`, der zweite Parameter `'w'` zeigt an, dass die Textdatei im Schreibmodus geöffnet werden soll. Sobald der Parameter `'w'` an die `open()` Funktion übergeben wird, kann die `.write()` Methode innerhalb der Funktion verwendet werden. In Python schreibt die `.write()` Methode einen String in eine vorgegebene Datei und ersetzt dabei den vorhandenen Dateiinhalt.

In diesem Fall wendet der Algorithmus die `.write()` Methode auf die in der `with` Anweisung angegebene Variable `file` an und übergibt die Allow-Liste `ip_addresses` als Argument. Damit überschreibt die `.write()` Methode den Inhalt der Textdatei `'allow_list.txt'` mit der überarbeiteten Allow-Liste `ip_addresses`. Auf diese Weise sind die zugangsbeschränkten Inhalte für diejenigen IP-Adressen, die aus der Allow-Liste entfernt wurden, nicht mehr zugänglich.

## Zusammenfassung

In diesem Projekt habe ich einen Python-Algorithmus entwickelt, der automatisch eine Textdatei mit IP-Adressen aktualisiert.

Die Textdatei `'allow_list.txt'` enthält die Allow-Liste mit den IP-Adressen, die auf die zugangsbeschränkten Inhalte im Unternehmensnetzwerk zugreifen dürfen. Als erstes öffnet der Algorithmus die Textdatei und liest den Inhalt im String-Format ein. Danach wird der String in eine Liste umgewandelt und der Variablen `ip_addresses` zugewiesen.

Anschließend durchläuft der Algorithmus in einer `for` Schleife die Remove-Liste `remove_list`. Die Remove-Liste enthält die IP-Adressen, die von der Allow-Liste entfernt werden sollen. Der Algorithmus überprüft für jedes Element in der Remove-Liste, ob es in der Allow-Liste enthalten ist, und entfernt es gegebenenfalls von dieser mit der `.remove()` Methode.

Im nächsten Schritt wendet der Algorithmus die `.join()` Methode an, um die Allow-Liste `ip_addresses` wieder in einen String umzuwandeln. Zum Schluss überschreibt der Algorithmus den Inhalt der Textdatei `'allow_list.txt'` mit der überarbeiteten Allow-Liste `ip_addresses` mit Hilfe der `.write()` Methode.

```Python
# Weise den Dateinamen `import_list.txt` der Variablen import_file zu.

import_file = 'allow_list.txt'

# Erstelle eine `with` Anweisung, um den Inhalt der Datei einzulesen.

with open(import_file, 'r') as file:

	# Verwende die `.read()` Methode, um den Inhalt der importierten Datei zu lesen, und weise ihn der Variable `ip_addresses` zu.
	
	ip_addresses = file.read()

# Gib den Inhalt der Allow-Liste aus.

print(ip_addresses)

# Verwende die `.split()` Methode, um den String `ip_addresses` in eine Liste umzuwandeln.

ip_addresses = ip_addresses.split()

# Erstelle eine `for` Schleife,
# nenne die Schleifenvariable `element`
# und durchlaufe die Liste 'remove_list'.

for element in remove_list:

	# Erstelle eine `if` Bedingung, um zu prüfen, ob `element` in `ip_addresses` enthalten ist.

	if element in ip_addresses:

		# Verwende die `.remove()` Methode, um Elemente von der Liste `ip_addresses` zu entfernen.

		ip_addresses.remove(element)

# Wandel die Allow-Liste `ip_addresses` wieder in einen String, damit es in die Textdatei geschrieben werden kann.

ip_addresses = '\n'.join(ip_addresses)

# Erstelle eine `with` Anweisung, um die Textdatei zu aktualisieren.

with open(import_file, 'w') as file:

	# Überschreibe den Inhalt der Textdatei mit der aktualisierten Liste `ip_addresses`.

	file.write(ip_addresses)

# Gib den Inhalt der überarbeiteten Allow-Liste aus.

print(ip_addresses)
```
