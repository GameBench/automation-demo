```
docker-compose up -d
```

Navigate to http://localhost:8090

## Build list

![Build list](/build-list.png)

## Plot

![Plot](/plot.png)

## Jenkinsfile

```groovy
node {
   stage('Test') {
       sh '''
       # launch app on device
       /Android/platform-tools/adb shell cmd activity start-activity -n $PACKAGE_NAME/.GoogleActivity

       export GBA_BASE_URL=http://localhost:8000

       # start recording a session
       SESSION_ID=$(gba-client session start $DEVICE_ID $PACKAGE_NAME)

       # sleep for 20 seconds
       sleep 20

       # stop recording session
       gba-client session stop --output-json $SESSION_ID > session.json

       /Android/platform-tools/adb shell am force-stop $PACKAGE_NAME

       echo "avg_fps" > data.csv
       cat session.json | jq -r '.summary.avg_fps' >> data.csv
       '''

       plot csvFileName: 'plot-8e54e334-ab7b-4c9f-94f7-b9d8965723df.csv',
        csvSeries: [[
            file: 'data.csv',
            exclusionValues: '',
            displayTableFlag: false,
            inclusionFlag: 'OFF',
            url: ''
        ]],
        group: 'Plot Group',
        title: 'Average FPS',
        style: 'line',
        exclZero: false,
        keepRecords: false,
        logarithmic: false,
        numBuilds: '',
        useDescr: false,
        yaxis: '',
        yaxisMaximum: '',
        yaxisMinimum: ''
   }
}
```

[Temple Run 2 example](templerun2)
