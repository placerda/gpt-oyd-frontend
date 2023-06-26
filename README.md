# gpt on your data frontend

## Build process

Everytime you change frontend code you need to build it before a new deployment:

```
cd frontend
npm install
npm run build
```

## Deploy to Azure

**1) Deployment pre-requirements**

- Deploy the Chatbot orchestrator in a Function App.

- Provision an Azure Speech Service for the speech to text and text to speech part.

**2) Create Web App**

Create a Web App (App Service) with Python 3.10 runtime.

**3) Set Startup Command**

In Azure Portal > Web App > Configuration > General Settings > Startup Command add:

```python ./app.py```

**4) Set Application Settings**

In Azure Portal > Web App > Configuration > Application Settings:

Add the application settings listed on [.env.template](.env.template), adjusting values accordingly to your environment.

**5) Deploy to Azure** (tthis step can be repeated whenever you make changes to the front)

In VSCode with [Azure Web App Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) go to the *Azure* Window, reveal your Web App in the resource explorer, right-click it then select *Deploy to Web App*.


## Frontend customizations

**1) Blob storage path**

Update the blob storage path in the getCitationFilePath function to point to where your data is.

file: ```frontend/src/api/api.ts```

Example: storage account ```177960botistorage``` and storage container ```documents```
```
export function getCitationFilePath(citation: string): string {
    return `https://177960botistorage.blob.core.windows.net/documents/${citation}`;
}
```

**2) Title**

Update page's title

file: ```frontend/src/pages/layout/Layout.tsx```

```
<h4 className={styles.headerRightText}>Chat On Your Data/h4>
```

file: ```frontend/src/pages/layout/index.html```

```
<title>Chat Chat On Your Data | Demo</title>
```

**3) Logo**

Update frontend logo

file: ```frontend/src/pages/layout/Layout.tsx```

Example:
```
<Link to="/" className={styles.headerTitleContainer}>
    <img height="80px" src="https://www.yourdomain.com/yourlogo.png"></img>
    <h3 className={styles.headerTitle}></h3>
</Link>
```

**4) Speech Synthesis**

To enable speech synthesis change speechSynthesisEnabled variable to true.

file: ```frontend/src/pages/chat/Chat.tsx```

```
const speechSynthesisEnabled = true;
```

