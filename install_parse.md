#### Installation: NodeJS 5, NPM 3, Git 2, parse-server, PM2
Install NodeJS 5
```
curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
sudo apt-get install -y nodejs
```
Upgrade NPM to latest version
```
sudo npm install npm@latest -g
```
Install Git 2
```
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update && sudo apt-get install git
```
Install Parse Server, Parse Dashboard, and PM2 Globally
```
sudo npm install -g parse-server parse-dashboard pm2
```
#### Configuration
Create user parse
```
sudo useradd --create-home --system parse
```
Make password for user parse
```
sudo passwd parse
```
Change login to parse
```
sudo su parse
```
Go to home directory
```
cd ~
```
Create cloud directory
```
mkdir -p ~/cloud
```
Create main.js
```
nano ~/cloud/main.js
```
create sample function in ~/cloud/main.js
```
Parse.Cloud.define('hello', function(req, res) {
  res.success('Hi');
});
```
Create ecosystem.json
```
nano ecosystem.json
```
Paste this script into ecosystem.json
```
{
  "apps" : [{
    "name"        : "parse-dashboard",
    "script"      : "/usr/bin/parse-dashboard",
    "watch"       : true,
    "merge_logs"  : true,
    "cwd"         : "/home/parse",
    "args"        : "--config=/home/parse/parse-dashboard-config.json --allowInsecureHTTP=1 --host=127.0.0.1 --port=4040 --mountPath=/dashboard"
  },{
    "name"        : "parse-wrapper",
    "script"      : "/usr/bin/parse-server",
    "watch"       : true,
    "merge_logs"  : true,
    "cwd"         : "/home/parse",
    "env": {
      "PARSE_SERVER_CLOUD_CODE_MAIN": "/home/parse/cloud/main.js",
      "PARSE_SERVER_DATABASE_URI": "mongodb://parse:password@your_domain_name:27017/database_name?ssl=true",
      "PARSE_SERVER_APPLICATION_ID": "your_application_id",
      "PARSE_SERVER_MASTER_KEY": "your_master_key",
      "PORT" : "1337",
      "HOST" : "127.0.0.1",
      "PARSE_SERVER_MOUNT_PATH" : "/parse"
    }
  }]
}
```
Create file parse-dashboard-config.json, and paste this script
```
{
  "apps": [
    {
      "serverURL": "http://apache-server/parse", // configure apache proxy to parse-server
      "appId": "your_application_id",
      "masterKey": "your_master_key",
      "appName": "MyTestApp"
    }
  ],
  "users": [
    {
      "user":"admin",
      "pass":"password"
    }
  ]
}
```
Edit /usr/lib/node_modules/parse-server/lib/cli/parse-server.js, and add HOST configuration
```
...
var server = app.listen(options.port, process.env.HOST || '0.0.0.0', function () {
...
```
#### Setup file adapter using S3 Amazon (Optional)
Install S3 Adapter
```
sudo npm install -g parse-server-s3-adapter
```
Add config in env :
```
    "env": {
      ....
      "PARSE_SERVER_FILES_ADAPTER": "parse-server-s3-adapter",
      "S3_ACCESS_KEY": "#########",
      "S3_SECRET_KEY": "#########",
      "S3_BUCKET": "my-bucket-parse-development",
      ....
    }
```
Edit /usr/lib/node_modules/parse-server/lib/cli/parse-server.js, add 'create S3Adapter object if FILES_ADAPTER is S3' code
```
...
if (!options.appId || !options.masterKey || !options.serverURL) {
  ...
}

// create S3Adapter object if FILES_ADAPTER is S3
if ('parse-server-s3-adapter' == process.env.PARSE_SERVER_FILES_ADAPTER) {
  options.filesAdapter = new _index.S3Adapter({
        accessKey: process.env.S3_ACCESS_KEY || '',
        secretKey: process.env.S3_SECRET_KEY || '',
        bucket: process.env.S3_BUCKET || '',
        region: process.env.S3_REGION || ''
  });
}

var app = (0, _express2.default)();
var api = new _index.ParseServer(options);
...
```
#### Start parse-server as daemon
```
pm2 start ecosystem.json
pm2 save
exit
```
#### Setup parse-server to run automatic when startup 
```
sudo pm2 startup ubuntu -u parse --hp /home/parse/
```
#### Test hello
```
curl -X POST \
     -H "X-Parse-Application-Id: your_application_id" \
     -H "Content-Type: application/json" -d '{}' \
     http://localhost:1337/parse/functions/hello
```
