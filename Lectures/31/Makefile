

all: Lect-31.html Lect-32.html Homework-Marlowe.html

FR=../01/

Lect-31.html: Lect-31.md
	markdown-cli --input=./Lect-31.md --output=Lect-31.html
	cat ${FR}/css/pre ${FR}/css/markdown.css ${FR}/css/post ../../md.css ${FR}/css/hpre Lect-31.html ${FR}/css/hpost >/tmp/Lect-31.html
	mv /tmp/Lect-31.html ./Lect-31.html

Lect-32.html: Lect-32.md
	markdown-cli --input=./Lect-32.md --output=Lect-32.html
	cat ${FR}/css/pre ${FR}/css/markdown.css ${FR}/css/post ../../md.css ${FR}/css/hpre Lect-32.html ${FR}/css/hpost >/tmp/Lect-32.html
	mv /tmp/Lect-32.html ./Lect-32.html


Homework-Marlowe.html: Homework-Marlowe.md
	markdown-cli --input=./Homework-Marlowe.md --output=Homework-Marlowe.html
	cat ${FR}/css/pre ${FR}/css/markdown.css ${FR}/css/post ../../md.css ${FR}/css/hpre Homework-Marlowe.html ${FR}/css/hpost >/tmp/Homework-Marlowe.html
	mv /tmp/Homework-Marlowe.html ./Homework-Marlowe.html


#Homework-Marlow.md
