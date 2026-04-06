# Chatla SDK for Unity (Source)

This is the **source code** repository for the Chatla Unity SDK.

The public distribution (precompiled DLLs) is at: https://github.com/Simply-Expert/chatla-unity

## Development

### Building

```bash
cd Build
dotnet build ChatlaSdk.Runtime.csproj -c Release
dotnet build ChatlaSdk.Editor.csproj -c Release
```

Output DLLs go to `dist/Runtime/` and `dist/Editor/`.

### Publishing a new version

```bash
./publish.sh 1.0.3
```

This will:
1. Update `package.json` version
2. Build both DLLs
3. Clone the public dist repo
4. Copy DLLs + package.json + README
5. Commit, tag, and push

### Users install via

```
https://github.com/Simply-Expert/chatla-unity.git?path=ChatlaSdk#v1.0.2
```
