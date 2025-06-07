# AES
Java Dependency (OpenJDK for LanguageTool) 
LanguageTool (via language_tool_python) requires Java (JRE/JDK) on the server. 
Render.com and most cloud platforms do not install Java by default. 
On Render, you can add a build script or a start command to install Java before starting your app. 
 
Example for Render: 
 
apt-get update && apt-get install -y openjdk-21-jre 
 
In your Render dashboard, set the build command to: 
Or, if using a render.yaml, add: 
 
buildCommand: | 
  apt-get update 
  apt-get install -y openjdk-21-jre 
 
Note: You do NOT add the .msi installer to your repo. The server must install Java using Linux commands. 
