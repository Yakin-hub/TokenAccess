    public string GenerateAccessToken()
    {
        using (HttpClient client = new HttpClient())
        {
            var clientId = "HR_PO";
            //var clientSecret = "TQVRilf_faYuGBCHqcNKyok4v15eJbhTuQf77xyjehA";
            var clientSecret = "upOgB87RaB1NKX8G0K6LMUlUELEAP2SPo-a37bzW9GE";
            var scope = "LocalPO|MUM_GIS|CC_SEND_REST_GIS_Token";

            //var tokenUrl = "https://issdev.adanielectricity.com/RESTAdapter/OAuthServer";

            var tokenUrl = "https://iss.adanielectricity.com/RESTAdapter/OAuthServer";

            var content = new FormUrlEncodedContent(new Dictionary<string, string>
            {
                { "client_id", clientId },
                { "client_secret", clientSecret },
                { "grant_type", "client_credentials" },
                { "scope", scope }
            });

            var response = client.PostAsync(tokenUrl, content).Result;
            var tokenResponse = response.Content.ReadAsStringAsync().Result;
            return tokenResponse;
        }
    }

                tokenData = GenerateAccessToken();
  using (HttpClient client = new HttpClient())
                    {

                        //string tokenData = GenerateAccessToken();
                        var tokenObj = JsonConvert.DeserializeObject<JObject>(tokenData);
                        var accessToken = tokenObj.Value<string>("access_token");

                        // Set the access token

                        client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);

                         string JsonData = Newtonsoft.Json.JsonConvert.SerializeObject(nonExe_Payment);
                        var content = new StringContent(JsonData, Encoding.UTF8, "application/json");
                        HttpResponseMessage response = client.PostAsync(baseUrl, content).Result;

                        ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12;

                        if (response.IsSuccessStatusCode)
                        {
                            // Read and process the response

                            string responseBody = response.Content.ReadAsStringAsync().Result;

                            dynamic responseObject = Newtonsoft.Json.JsonConvert.DeserializeObject(responseBody);
}

https://www.aspsnippets.com/Articles/881/GridView-CRUD-Select-Insert-Edit-Update-Delete-using-Single-Stored-Procedure-in-ASPNet/
