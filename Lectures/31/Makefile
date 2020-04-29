

all: Lect-31.html

FR=../01/

Lect-31.html: Lect-31.md
	markdown-cli --input=./Lect-31.md --output=Lect-31.html
	cat ${FR}/css/pre ${FR}/css/markdown.css ${FR}/css/post ../../md.css ${FR}/css/hpre Lect-31.html ${FR}/css/hpost >/tmp/Lect-31.html
	mv /tmp/Lect-31.html ./Lect-31.html


