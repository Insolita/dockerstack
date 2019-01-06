# Simple self-signed ssl-key generation
# USAGE: make domain=sitename.app cert
cert:
	rm -f $(domain).conf && rm -f ssl/$(DOMAIN).key && rm -f ssl/$(domain).crt
	sed 's/__SITENAME__/$(domain)/g' cert.conf| tee $(domain).conf
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/$(domain).key \
-out ssl/$(domain).crt -config $(domain).conf \
-subj "/C=RU/ST=Russia/L=Bobruysk/O=Sofa development/OU=IT Department/CN=$(domain)"
	rm -f $(domain).conf