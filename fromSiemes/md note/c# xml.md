### xml  schema

~~~xml-dtd
<?xml version="1.0" encoding="utf-8"?>
<xs:schema targetNamespace="http://tempuri.org/01"
    elementFormDefault="qualified"
    xmlns="http://www.w3.org/2001/XMLSchema"
    xmlns:tns="http://tempuri.org/01"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
>

  <xs:element name="deviceList">
    <xs:complexType>
      <xs:sequence maxOccurs='unbounded'>
        <xs:element name="device">
          <xs:complexType>
            <xs:sequence>
              <xs:element name='ip' type='xs:string'></xs:element>
              <xs:element name='name' type='xs:string'></xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>

~~~

### xml 引用schema

~~~xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema targetNamespace="http://tempuri.org/01"
    elementFormDefault="qualified"
    xmlns="http://www.w3.org/2001/XMLSchema"
    xmlns:tns="http://tempuri.org/01"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
>

  <xs:element name="deviceList">
    <xs:complexType>
      <xs:sequence maxOccurs='unbounded'>
        <xs:element name="device">
          <xs:complexType>
            <xs:sequence>
              <xs:element name='ip' type='xs:string'></xs:element>
              <xs:element name='name' type='xs:string'></xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>

~~~

### C#读取xml

~~~c#
		    XmlDocument xmldoc = new XmlDocument();
            xmldoc.Load(IP_TO_NAME_CONFIG);
            XmlNode deviceList = xmldoc.LastChild;
            XmlNodeList list = deviceList.ChildNodes;
            foreach (XmlElement node in list)
            {
                string name = node.GetElementsByTagName("name")[0].InnerText;
                string ip = node.GetElementsByTagName("ip")[0].InnerText;
                IpToDeviceNameDictionary.Add(ip, name);
            }
~~~



