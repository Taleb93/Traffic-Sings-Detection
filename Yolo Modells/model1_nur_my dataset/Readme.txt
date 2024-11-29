Das Modell wurde mit Yolov8 trainiert
mit folgende Augmentieren während des trainigs:

!yolo task=detect mode=train model=yolov8n.pt data=/content/HRW_Relevant-1/data.yaml epochs=50 batch=16 \
lr0=0.01 lrf=0.2 momentum=0.937 weight_decay=0.0005 warmup_epochs=3.0 \
hsv_h=0.02 hsv_s=0.8 hsv_v=0.5 degrees=5.0 translate=0.2 scale=0.8 shear=0.2 mosaic=1.0 mixup=0.2




Erkärung:
lr0=0.01 (Initiale Lernrate)
Was es macht: Bestimmt die anfängliche Lernrate des Modells. Eine höhere Lernrate lässt das Modell schneller lernen, kann aber instabil sein.
Warum 0.01?:
Dies ist die empfohlene Standard-Lernrate für YOLO. Sie sorgt für schnelles Lernen in den ersten Epochen und wurde getestet, um robust zu sein.
lrf=0.2 (Finale Lernrate als Faktor)
Was es macht: Die Lernrate wird mit jeder Epoche reduziert. Am Ende des Trainings wird die Lernrate lr0 * lrf.
Warum 0.2?:
Dies ermöglicht dem Modell, am Ende des Trainings feinere Anpassungen vorzunehmen, ohne die gelernten Parameter drastisch zu ändern.
momentum=0.937
Was es macht: Momentum hilft dem Optimierungsalgorithmus, sich "flüssiger" in Richtung des Optimums zu bewegen, indem vorherige Gradienten berücksichtigt werden.
Warum 0.937?:
Dies ist ein bewährter Wert, der für YOLO-Modelle gut funktioniert, da er schnell lernt und gleichzeitig Schwankungen reduziert.
weight_decay=0.0005
Was es macht: Verhindert Überanpassung (Overfitting), indem es Gewichte des Modells leicht bestraft, die zu groß werden.
Warum 0.0005?:
Standardwert für YOLO. Gut geeignet, um das Modell zu regulieren, ohne das Training zu stark zu beeinflussen.
warmup_epochs=3.0
Was es macht: Langsamer Anstieg der Lernrate in den ersten Epochen, um das Training stabil zu starten.
Warum 3.0?:
Drei Epochen reichen aus, um das Modell auf die volle Lernrate vorzubereiten, ohne Zeit zu verschwenden.
2. Augmentierungsparameter
Augmentierungen erhöhen die Vielfalt der Trainingsdaten durch Transformationen wie Farbänderungen, Skalierung, Verschiebung usw. Dies hilft, ein robusteres Modell zu trainieren, das sich besser auf neue Daten verallgemeinern lässt.

hsv_h=0.02 (Farbtonänderung)
Was es macht: Verschiebt den Farbton (Hue) des Bildes, z. B. Ampelgrün könnte etwas heller oder dunkler wirken.
Warum 0.02?:
Verkehrszeichen und Ampeln basieren oft auf Farben. Eine leichte Verschiebung macht das Modell robuster gegenüber Beleuchtungsunterschieden.
hsv_s=0.8 (Sättigungsänderung)
Was es macht: Verändert die Farbintensität (Sättigung) der Bilder.
Warum 0.8?:
Dies erzeugt realistischere Variationen, z. B. verblasste oder überbelichtete Verkehrszeichen.
hsv_v=0.5 (Helligkeitsänderung)
Was es macht: Verändert die Helligkeit des Bildes.
Warum 0.5?:
Verkehrszeichen und Ampeln können je nach Tageszeit unterschiedlich beleuchtet sein. Dies hilft dem Modell, mit solchen Variationen umzugehen.
degrees=5.0 (Rotationsänderung)
Was es macht: Rotiert das Bild leicht.
Warum 5.0?:
Verkehrszeichen und Schilder können leicht schräg montiert oder aus einem anderen Winkel fotografiert sein. Kleine Rotationen verbessern die Robustheit.
translate=0.2 (Verschiebung des Bildes)
Was es macht: Verschiebt das Bild horizontal oder vertikal.
Warum 0.2?:
Verkehrszeichen erscheinen nicht immer zentriert im Bild. Eine Verschiebung simuliert solche realen Szenarien.
scale=0.8 (Skalierung)
Was es macht: Verändert die Größe des Bildes, z. B. durch Verkleinerung oder Vergrößerung.
Warum 0.8?:
Verkehrszeichen sind in verschiedenen Entfernungen sichtbar. Diese Skalierung macht das Modell robuster gegenüber Größenunterschieden.
shear=0.2 (Schräge Verzerrung)
Was es macht: Verzieht das Bild leicht diagonal.
Warum 0.2?:
Verkehrszeichen können aufgrund der Kameraperspektive schräg erscheinen. Dies hilft, das Modell für solche Szenarien zu trainieren.
3. Spezielle Augmentierungsstrategien
mosaic=1.0 (Mosaik-Augmentierung)
Was es macht: Kombiniert mehrere Bilder in einem einzigen Bild. Dies erhöht die Anzahl der Objekte pro Bild und bietet mehr Vielfalt.
Warum 1.0?:
Mosaik ist eine Schlüsselstrategie für YOLO-Modelle, da es die Datenmenge effektiv erhöht und die Modellrobustheit verbessert.
mixup=0.2 (Mixup-Augmentierung)
Was es macht: Kombiniert zwei Bilder miteinander, indem es Pixelwerte mischt.
Warum 0.2?:
Mixup hilft, das Modell robuster gegenüber Rauschen und ungewöhnlichen Bildkombinationen zu machen. Der Wert von 0.2 stellt sicher, dass es nicht zu oft angewendet wird.
Warum diese Werte?
Die Werte basieren auf den Standards und bewährten Verfahren von YOLO für realistische Datenaugmentierungen.
Sie wurden so gewählt, dass sie Verkehrszeichen und Ampelszenarien besser abdecken, indem sie Variationen in Beleuchtung, Position, Perspektive und Größe simulieren.
Zusammenfassung der Zielsetzung
Lernparameter: Stabilität und schnelles Lernen in den ersten Epochen, gefolgt von feiner Anpassung am Ende.
Augmentierungen: Simulation realistischer Szenarien, in denen Verkehrszeichen leicht unterschiedlich aussehen können.
Robustheit: Vermeidung von Überanpassung und bessere Generalisierung auf neue Daten.
