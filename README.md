
# 🚀 Request Logger Demo (ASP.NET Core Web API)

This project demonstrates how to implement a **custom middleware** in **ASP.NET Core** that logs incoming HTTP requests and outgoing responses.  

The middleware logs:
- Request **HTTP Method** (e.g., `GET`, `POST`)
- Request **Path/URL**
- Response **Status Code**

---

## 📌 Features
- ✅ Custom middleware implementation (`RequestLoggingMiddleware`)  
- ✅ Extension method for easy registration (`UseRequestLogging`)  
- ✅ Integrated into the middleware pipeline (`Program.cs`)  
- ✅ Logs request/response details to console or configured logger  
- ✅ Example API (`WeatherForecastController`) to test logging  

---

## 🏗️ Project Structure
```
RequestLoggerDemo/
│
├── Controllers/
│   └── WeatherForecastController.cs    # Sample controller
│
├── Middleware/
│   └── RequestLoggingMiddleware.cs     # Custom logging middleware
│
├── Program.cs                          # App entry point & middleware registration
├── RequestLoggerDemo.csproj            # Project file
└── README.md                           # Documentation
```

---

## ⚙️ How It Works
### 🔹 Middleware Flow
1. **Incoming request** → Logged by middleware  
2. **Request passes** to next middleware (e.g., controllers)  
3. **Response is returned** → Logged before leaving  

### 🔹 Example Logs
```
➡️ Incoming Request: GET /WeatherForecast
⬅️ Outgoing Response: 200
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```sh
git clone https://github.com/<your-username>/RequestLoggerDemo.git
cd RequestLoggerDemo
```

### 2. Open in Visual Studio
- Open `RequestLoggerDemo.sln` in **Visual Studio 2022+**

### 3. Run the Application
- Press **F5** or run:
```sh
dotnet run
```

### 4. Test the API
- Open Swagger UI at:  
  👉 `https://localhost:5001/swagger` (or the port shown in your console)  

- Call `GET /WeatherForecast` → Check logs in **Console/Output window**  

---

## 📂 Code Snippets

### 🔹 Middleware
```csharp
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<RequestLoggingMiddleware> _logger;

    public RequestLoggingMiddleware(RequestDelegate next, ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation("➡️ Incoming Request: {method} {url}", 
            context.Request.Method, context.Request.Path);

        await _next(context);

        _logger.LogInformation("⬅️ Outgoing Response: {statusCode}", 
            context.Response.StatusCode);
    }
}
```

### 🔹 Register Middleware
```csharp
app.UseRequestLogging();
```

---

## 🛠️ Technologies Used
- [.NET 9](https://dotnet.microsoft.com/) (works with .NET 6/7/8 as well)  
- [ASP.NET Core Web API](https://learn.microsoft.com/en-us/aspnet/core)  
- [Swagger / Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore)  

---

## 📖 Future Enhancements
- Log request **headers** and **body**  
- Log response **body**  
- Write logs to **file or database** (using `Serilog` or `NLog`)  
- Add **correlation ID** for distributed tracing  

---

## 👨‍💻 Author
**Parth Patel**  
🔗 [LinkedIn](https://linkedin.com/in/imparthgalani)  
🔗 [GitHub](https://github.com/imparthgalani)  

---

✅ This project is a simple yet powerful example of **ASP.NET Core middleware** and how it can be used to customize the **HTTP request pipeline**.  
