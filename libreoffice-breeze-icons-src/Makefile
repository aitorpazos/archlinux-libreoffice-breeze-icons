# It builds icon packages ready to be copied to /usr/lib/libreoffice/share/config
#
VERSION=2015.8.8

all: images_breeze.zip images_breeze_dark.zip
	tar -cvzf libreoffice-breeze-icons-$(VERSION).tar.gz *.zip
	
plasma-next-icons:
	git clone https://github.com/NitruxSA/plasma-next-icons.git

%.zip: plasma-next-icons
	cd plasma-next-icons/LibreOffice_Breeze/ && \
	  make clean all && \
	  cp *.zip ../../

clean:
	rm -rf plasma-next-icons
	rm -f images_breeze.zip 
	rm -f images_breeze_dark.zip 
	rm -f libreoffice-breeze-icons-$(VERSION).tar.gz 

