# 🌀 Onatrix

**Onatrix** is a content-driven web platform built with **ASP.NET Core** and **Umbraco CMS**.  
It leverages the flexibility of Umbraco with the power of .NET to create a dynamic, easily managed website experience.

---

## 🚀 Features

- 💡 CMS-powered content using Umbraco
- ⚙️ Built with ASP.NET Core (.NET 10)
- 🔧 Structured folder setup with `Models`, `Views`, and `Controllers`
- 🌐 Responsive front-end layout
- 🧩 Extendable through uSync configurations

---

## 📂 Project Structure

```

Onatrix/
├── Models/                    # Custom view models
├── Views/                     # Razor views
├── wwwroot/                   # Static files (CSS, JS, images)
├── umbraco/                   # CMS data
├── uSync/                     # Umbraco sync config (optional)
├── Program.cs                 # Entry point
├── appsettings.json           # Configuration
└── Onatrix.csproj             # Project file

```

---

## 🛠️ Getting Started

1. **Install prerequisites**:
   - [.NET SDK 8](https://dotnet.microsoft.com/en-us/download)
   - [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) or LocalDB
   - [Visual Studio 2022+](https://visualstudio.microsoft.com/) (recommended)

2. **Restore and run**:
   ```bash
   dotnet restore
   dotnet run --project onatrix/onatrix.csproj
```

3. Open your browser and go to:
   `http://localhost:5000` or `https://localhost:5001`

---

## 🧠 Notes

* This project uses **Umbraco CMS**, which provides an admin dashboard at `/umbraco`.
* You can configure your connection string in `appsettings.json`.
* If you're deploying, make sure to exclude:

  * `/bin/`, `/obj/`, `.vs/`, `*.user` files from version control.

---

📄 License
This project was created as part of a course assignment at EC Utbildning. It is available for educational or demonstration purposes only. 

---

> Created by **Nour** — .NET Fullstack Developer & 3D Visual Designer


## Maintenance update — 2026-10-19

The project now targets **.NET 10** and **Umbraco CMS 17.7.1 (LTS)**. See [upgrade and validation notes](docs/upgrade-notes.md) for dependency changes, verification, and the remaining ImageSharp advisories.

The retired Azure database was not contacted or migrated. A successful build validates source compatibility, not restoration of the old content database or a working deployed site.
