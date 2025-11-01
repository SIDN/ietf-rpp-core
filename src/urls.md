-- Generic pattern
/domains/{tld}/{domain.name}
/contacts/{contact_id}

.example and .foo shared
Root URL: https://rpp.example/
https://rpp.example/domains/example/{domain.name}
https://rpp.example/domains/foo/{domain.name}
/contacts/{contact_id}


/contacts/net/ct12345
/contacts/com/ct12345


.bar and .buz not shared
Root URL .example: https://rpp.example/example
https://rpp.example/example/    domains/bar/{domain.name}
https://rpp.example/example/    contacts/{contact_id}

Root URL .foo: https://rpp.foo
https://rpp.foo/    domains/buz/{domain.name}
https://rpp.foo/    contacts/{contact_id}


Proxy
https://rpp.proxy.example/

https://rpp.proxy.example  /domains/foo/* -> https://rpp.example/domains/foo/*
https://rpp.proxy.example  /domains/buz/* -> https://rpp.foo/domains/buz/*
https://rpp.proxy.example  /contact/foo/* -> ?????

https://rpp.proxy.example/tld/...


route('/domains/{domainname})
route('/tlds/{tld}/domains/{domainname})
