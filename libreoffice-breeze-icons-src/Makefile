# It builds icon packages ready to be copied to /usr/lib/libreoffice/share/config
#
VERSION=2015.5.4

all: images_breeze.zip images_breeze_dark.zip
	tar -cvzf libreoffice-breeze-icons-$(VERSION).tar.gz *.zip
	
plasma-next-icons:
	git clone https://github.com/NitruxSA/plasma-next-icons.git

%.png: plasma-next-icons
	mkdir -p breeze
	mkdir -p breeze_dark
	cd plasma-next-icons/LibreOffice_Breeze/breeze/ && \
	for f in `find . -not -type l -name "*.svg"`; do \
		newf="../../../breeze/`echo $$f | sed 's#.svg#.png#g'`"; \
		newf_dark="../../../breeze_dark/`echo $$f | sed 's#.svg#.png#g'`"; \
		mkdir -p `dirname $$newf` `dirname $$newf_dark`; \
		convert -background none -size 16x16 "$$f" "$$newf"; \
		cat "$$f" | sed -e 's/#4d4d4d/#f2f2f2/gI' | sed -e 's/#adadad/#f9f9f9/gI' \
		    | convert -background none -size 16x16 - "$$newf_dark"; \
	done && \
	for f in `find . -type l -name "*.svg"`; do \
		filelink="`readlink $$f | sed 's#.svg#.png#g'`"; \
		filename="`basename $$f | sed 's#.svg#.png#g'`"; \
		newf="../../../breeze/`dirname $$f`"; \
		newf_dark="../../../breeze_dark/`dirname $$f`"; \
		mkdir -p "$$newf" "$$newf_dark"; \
		$$(cd $$newf ; ln -s "$$filelink" "$$filename"); \
		$$(cd $$newf_dark ; ln -s "$$filelink" "$$filename"); \
	done && \
	for f in `find . -not -type d -not -name "*.svg"`; do \
		newf="../../../breeze/$$f"; \
		newf_dark="../../../breeze_dark/$$f"; \
		mkdir -p "`dirname $$newf`" "`dirname $$newf_dark`"; \
		cp -d "$$f" "$$newf"; \
		cp -d "$$f" "$$newf_dark"; \
	done
	
images_breeze.zip images_breeze_dark.zip: %.png
	cd breeze && zip -y -r ../images_breeze.zip *
	cd breeze_dark && zip -y -r ../images_breeze_dark.zip *

clean:
	rm -rf breeze
	rm -rf breeze_dark
	rm -rf plasma-next-icons
	rm -f images_breeze.zip 
	rm -f images_breeze_dark.zip 
	rm -f libreoffice-breeze-icons-$(VERSION).tar.gz 

