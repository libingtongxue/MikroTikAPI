# MikroTikAPI<br/>
MikroTikAPI<br/>
<br/>
<br/>
        static void Main(string[] args)<br/>
        {<br/>
            MK MK = new MK("192.168.112.1");<br/>
            if (MK.Login("admin", "87488587"))<br/>
            {<br/>
                MK.Send("/system/resource/print");<br/>
                //MK.Send("=.proplist=uptime");<br/>
                MK.Send(".tag=resource", true);<br/>
                foreach (string t in MK.Read())<br/>
                {<br/>
                    if (t.StartsWith("!re"))<br/>
                    {<br/>
                        string data = t.Substring(16);<br/>
                        <br/>
                        foreach(var s in GetDictionary(data))<br/>
                        {<br/>
                            Console.WriteLine("{0}:{1}", s.Key, s.Value);<br/>
                        }<br/>
                    }<br/>
                }<br/>
            }<br/>
            else<br/>
            {<br/>
                Console.WriteLine("Can't Login In");<br/>
            }<br/>
            MK.Close();<br/>
        }<br/>
        <br/>
        public static Dictionary<string,string> GetDictionary(string data)<br/>
        {<br/>
            List<string> keys = new List<string>();<br/>
            List<string> values = new List<string>();<br/>
            string[] datas = data.Split("=");<br/>
            for (int i = 1; i < datas.Length; i++)<br/>
            {<br/>
                if (i % 2 == 1)<br/>
                {<br/>
                    keys.Add(datas[i]);<br/>
                }<br/>
                else<br/>
                {<br/>
                    values.Add(datas[i]);<br/>
                }<br/>
            }<br/>
            Dictionary<string, string> keyValuePairs = new Dictionary<string, string>();<br/>
            for (int i = 0; i < keys.Count; i++)<br/>
            {<br/>
                keyValuePairs.Add(keys[i], values[i]);<br/>
            }<br/>
            return keyValuePairs;<br/>
        }<br/>