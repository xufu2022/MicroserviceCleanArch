# MicroserviceCleanArch

--set up

dotnet new sln --name EShopping --force
dotnet new webapi -n Catalog.API -o Services/Catalog/Catalog.API
dotnet new classlib -n Catalog.Core -o Services/Catalog/Catalog.Core
dotnet new classlib -n Catalog.Application -o Services/Catalog/Catalog.Application
dotnet new classlib -n Catalog.Infrastructure -o Services/Catalog/Catalog.Infrastructure
dotnet new classlib -n Common.Logging -o Infrastructure/Common.Logging

dotnet sln EShopping.sln add Services/Catalog/Catalog.API/Catalog.API.csproj
dotnet sln EShopping.sln add Services/Catalog/Catalog.Core/Catalog.Core.csproj
dotnet sln EShopping.sln add Services/Catalog/Catalog.Application/Catalog.Application.csproj
dotnet sln EShopping.sln add Services/Catalog/Catalog.Infrastructure/Catalog.Infrastructure.csproj
dotnet sln EShopping.sln add Infrastructure/Common.Logging/Common.Logging.csproj

dotnet add Services/Catalog/Catalog.Infrastructure/Catalog.Infrastructure.csproj reference Services/Catalog/Catalog.Application/Catalog.Application.csproj
dotnet add Services/Catalog/Catalog.Application/Catalog.Application.csproj reference Services/Catalog/Catalog.Core/Catalog.Core.csproj
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj reference Services/Catalog/Catalog.Infrastructure/Catalog.Infrastructure.csproj
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj reference Services/Catalog/Catalog.Application/Catalog.Application.csproj
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj reference Infrastructure/Common.Logging/Common.Logging.csproj

dotnet add Services/Catalog/Catalog.Core/Catalog.Core.csproj package MongoDB.Driver
dotnet add Services/Catalog/Catalog.Core/Catalog.Core.csproj package AspNetCore.HealthChecks.MongoDb

dotnet add Services/Catalog/Catalog.Application/Catalog.Application.csproj package AutoMapper
dotnet add Services/Catalog/Catalog.Application/Catalog.Application.csproj package MediatR

dotnet add Services/Catalog/Catalog.Infrastructure/Catalog.Infrastructure.csproj package Microsoft.Extensions.Configuration.Binder

dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package AspNetCore.HealthChecks.UI.Client
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package AutoMapper.Extensions.Microsoft.DependencyInjection
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package MediatR.Extensions.Microsoft.DependencyInjection
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package Microsoft.AspNetCore.Mvc.Versioning.ApiExplorer
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package Microsoft.Extensions.DependencyInjection
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package Microsoft.Extensions.DependencyInjection.Abstractions
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package Microsoft.Extensions.Logging.Abstractions
dotnet add Services/Catalog/Catalog.API/Catalog.API.csproj package Microsoft.AspNetCore.Authentication.JwtBearer

dotnet add Infrastructure/Common.Logging/Common.Logging.csproj package Serilog.AspNetCore
dotnet add Infrastructure/Common.Logging/Common.Logging.csproj package Serilog.Enrichers.Environment
dotnet add Infrastructure/Common.Logging/Common.Logging.csproj package Serilog.Exceptions
dotnet add Infrastructure/Common.Logging/Common.Logging.csproj package Serilog.Sinks.Console
dotnet add Infrastructure/Common.Logging/Common.Logging.csproj package Serilog.Sinks.Elasticsearch

dotnet build
dotnet run --project Services/Catalog/Catalog.API/Catalog.API.csproj  --launch-profile "https"



dotnet run -- arg1 arg2 (passing argument)