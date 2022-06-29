# MikroTikAPI
````
        static void Main(string[] args)
        {
            MK MK = new MK("192.168.112.1");
            if (MK.Login("admin", "87488587"))
            {
                MK.Send("/system/resource/print");
                //MK.Send("=.proplist=uptime");
                MK.Send(".tag=resource", true);
                foreach (string t in MK.Read())
                {
                    if (t.StartsWith("!re"))
                    {
                        string data = t.Substring(16);
                        
                        foreach(var s in GetDictionary(data))
                        {
                            Console.WriteLine("{0}:{1}", s.Key, s.Value);
                        }
                    }
                }
            }
            else
            {
                Console.WriteLine("Can't Login In");
            }
            MK.Close();
        }
        
        public static Dictionary<string,string> GetDictionary(string data)
        {
            List<string> keys = new List<string>();
            List<string> values = new List<string>();
            string[] datas = data.Split("=");
            for (int i = 1; i < datas.Length; i++)
            {
                if (i % 2 == 1)
                {
                    keys.Add(datas[i]);
                }
                else
                {
                    values.Add(datas[i]);
                }
            }
            Dictionary<string, string> keyValuePairs = new Dictionary<string, string>();
            for (int i = 0; i < keys.Count; i++)
            {
                keyValuePairs.Add(keys[i], values[i]);
            }
            return keyValuePairs;
        }
````