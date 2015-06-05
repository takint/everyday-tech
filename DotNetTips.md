Enable Cross domail access for REST Api
	First Install:
		Install-Package Microsoft.AspNet.WebApi.Cors
	Then in WebApiConfig.cs add:
		config.EnableCors();
	Final Enable Cors wherever you want:
		[EnableCors(origins: "http://localhost:4200", headers: "*", methods: "get,post")]
	Done