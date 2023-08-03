# windows-event-schemas

I was looking for a compiled location of the Windows event logs XML schema and couldnt find it.

Decided to just pull this `https://github.com/MicrosoftDocs/windows-itpro-docs/tree/main/windows/security/threat-protection/auditing`
and then:
```python
import os
import glob
import re

def extract_event_xml(directory):
    for filename in glob.glob(os.path.join(directory, '*.md')):
        with open(filename, 'r') as file:
            content = file.read()
            # Look for the MarkDown ***Event XML*** 
            match = re.search(r'(?<=```)(.*?)(?=```)', content, re.DOTALL)
            if match:
                xml_content = match.group(0).strip()
                new_filename = os.path.splitext(filename)[0] + '-schema.xml'
                with open(new_filename, 'w') as new_file:
                    new_file.write(xml_content)

extract_event_xml('/path/to/your/directory')
```
