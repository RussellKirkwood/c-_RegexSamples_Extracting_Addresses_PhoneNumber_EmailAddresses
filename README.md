# c-_RegexSamples_Extracting_Addresses_PhoneNumber_EmailAddresses
C# Regex Samples to extract Address, Phone Numbers and Email Addresses


public List<string> ExtractAddressRegex(string text)
        {
            var extractedAddress = new List<string>();            
            string[] streetsArray = { "avenue", "ave", "lane", "ln", "boulevard", "blvd", "drive", "dr", "road", "rd", "street", "st", "str", "parkway", "pkway", "pkwy", "highway", "hway", "circle", "cir", "court", "ct" };                        

            var regexAddress1 = new Regex(@"\d{1,3}.?\d{0,3}\s[a-zA-Z]{2,30}\s[a-zA-Z]{2,15}", RegexOptions.Compiled | RegexOptions.IgnoreCase);

            MatchCollection matches = regexAddress.Matches(text);
            
            foreach (Match match in matches)
            {
                string[] addressSplit = match.Value.ToLower().Split(' ');

                var lastword = addressSplit.Last().ToLower();

                foreach (var word in streetsArray)
                {
                    if (word == lastword)
                    {
                        extractedAddress.Add(match.Value.ToString());
                    }
                }              
            }

            return extractedAddress;
        }

        public List<string> ExtractEmailRegex(string text)
        {
            var extractedEmail = new List<string>();

            const string MatchEmailPattern =
           @"(([\w-]+\.)+[\w-]+|([a-zA-Z]{1}|[\w-]{2,}))@"
           + @"((([0-1]?[0-9]{1,2}|25[0-5]|2[0-4][0-9])\.([0-1]?[0-9]{1,2}|25[0-5]|2[0-4][0-9])\."
             + @"([0-1]?[0-9]{1,2}|25[0-5]|2[0-4][0-9])\.([0-1]?[0-9]{1,2}|25[0-5]|2[0-4][0-9])){1}|"
           + @"([a-zA-Z]+[\w-]+\.)+[a-zA-Z]{2,4})";
            Regex rx = new Regex(MatchEmailPattern, RegexOptions.Compiled | RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1));
            // Find matches.
            MatchCollection matches = rx.Matches(text);
            // Report the number of matches found.
            //int noOfMatches = matches.Count;
            // Report on each match.
            foreach (Match match in matches)
            {
                extractedEmail.Add(match.Value.ToString());
            }

            return extractedEmail;
        }        

        public List<string> ExtractPhoneRegex(string text)
        {
            var extractedPhoneNumber = new List<string>();            

            var regexPhoneNumber = new Regex(@"((\(\d{3}\)?)|(\d{3}))([\s-./]?)(\d{3})([\s-./]?)(\d{4})", // North American
    RegexOptions.Compiled | RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1));    
            
            MatchCollection matches = regexPhoneNumber.Matches(text);

            
            foreach (Match match in matches)
            {
                extractedPhoneNumber.Add(match.Value.ToString());
            }

            return extractedPhoneNumber;
        }

        
    }
