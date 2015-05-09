# It builds icon packages ready to be copied to /usr/lib/libreoffice/share/config
#
VERSION=2015.5.1

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
		convert -background none -size 16x16 "$$f" -fill '#f2f2f2' -opaque '#4d4d4d'  "$$newf_dark"; \
	done && \
	for f in `find . -type -l or -not -name "*.svg"`; do \
		newf="../../../breeze/$$f"; \
		newf_dark="../../../breeze_dark/$$f"; \
		mkdir -p `dirname $$newf` `dirname $$newf_dark` \
		cp "$$f" "$$newf"; \
		cp "$$f" "$$newf_dark"; \
	done \
	
images_breeze.zip images_breeze_dark.zip: %.png
	cd breeze && zip -r ../images_breeze.zip *
	cd breeze_dark && zip -r ../images_breeze_dark.zip *

clean:
	rm -rf breeze;
	rm -rf breeze_dark;