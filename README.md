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
}
