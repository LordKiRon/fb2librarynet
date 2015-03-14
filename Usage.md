# Introduction #

Here is an example of loading FB2 file into FB2File class object:

```
        private bool LoadFB2File(string fileName)
        {
            try
            {
                Stream s = File.OpenRead(fileName);
                ReadFB2FileStream(s);
                s.Close();
            }
            catch (Exception)
            {
                return false;
            }
            return true;
        }


private void ReadFB2FileStream(Stream s)
        {
            XmlReaderSettings settings = new XmlReaderSettings
            {
                ValidationType = ValidationType.None,
                ProhibitDtd = false
            };
            XDocument fb2Document = null;
            using (XmlReader reader = XmlReader.Create(s, settings))
            {
                fb2Document = XDocument.Load(reader,LoadOptions.PreserveWhitespace);
                reader.Close();
            }
            FB2File file = new FB2File();
            try
            {
                file.Load(fb2Document,false);
            }
            catch (Exception ex)
            {
                Console.WriteLine(string.Format("Error loading file : {0}",ex.Message));
            }
        }


```