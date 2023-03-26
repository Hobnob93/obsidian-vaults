#azure #az-204 

**WADL**: Web Application Description Language.
**WSDL**: Web Services Description Language.
They are both XML files that describe REST web services.

| WADL                                                        | WSDL                                               |
| ----------------------------------------------------------- | -------------------------------------------------- |
| application                                                 | definition                                         |
| grammars                                                    | types                                              |
| Resource: `resources@base + resource@path`                  | Interface: `service::endpoint@address`             |
| Method: `@id, @name, @href`                                 | Operation: `@name, @pattern, @safe, @style ...`    |
| Request/Response: `::param@type` `::representation@element` | Input/Output: `@type`                              |
| Param: `@type`                                              | xds:element: `@element`                            |
| Param: `::option@value`                                     | xsd:simpleType: `::restriction::enumeration@value` |
