# Speech to Text

Note: This lab can be done either on a stand-alone system (using a local file or your microphone) or done on Bluemix uploading a WAV file using an upload node (Dropbox, Box...) or straight from an URL.

Speech to Text service can be used anywhere voice-interactivity is needed. The service is great for mobile experiences, transcribing media files, call centre transcriptions, voice control of embedded systems, or converting sound to text to then make data searchable. Supported languages include:
- US English
- Spanish
- Japanese
- Brazilian Portuguese
- Mandarin.

## On Bluemix

* Go to the Bluemix catalog and go to `Boilerplates` under Apps.
* If you don't already have one, create a `Internet of Things Platform Starter` application.
* Once created, you want to go to the `Connections` tab and click `Connect New`.
* Click on `Services` under Watson and click the `Speech to Text` service to add it to your application.
* Click on the service instance you've created, then go to the Service credentials tab and then click `Add Credentials` and `Add` in the new window. When prompted to restage your app, do so.
* Now that you've set up the service and connected it to your app, you're ready to create the Node red flow using the service.


### Uploading from a URL

![`S2TBluemixURLFlowOverview`](images/s2t_bluemix_url_overview.png)

In this lab an audio file will be transcribed. An example audiofile can be found [here](http://sd-2.archive-host.com/membres/up/102033098234604628/SpaceShuttle.wav), feel free to use this URL or to provide your own.

In the following screenshots you can see how the nodes are configured.

First you start with an Inject node that will provide the URL to our WAV file into the Speech To Text service in Bluemix

The inject node is configured like this:

![`S2TBluemixURLFlowinject`](images/s2t_bluemix_url_inject.png)

Change the payload `type` to string (click on the little arrow) and paste the following url into it:

  ```
  http://sd-2.archive-host.com/membres/up/102033098234604628/SpaceShuttle.wav
  ```

The next node is the Speech to Text node that will stream the .wav file from the URL provided and transcribe it.
This node is configured like this by default:

![`S2TFBluemixURLFlowS2T`](images/s2t_bluemix_url_s2t.png)

The file used as an example is in English but if you're providing your own file in a different language make sure to change it. You can also select the quality of your .wav file and chose whether you want the transcription to stop at the first pause detected or to keep going until the end of the file.
(Note: The continuous parameter is now working at the moment.)

The last node is the debug node that will allow you to see the results of the transcription, it is configured like this:

![`S2TBluemixURLFlowDebug`](images/s2t_bluemix_url_debug.png)

The output is set to msg.transcription so only the transcript is shown in the debug tab.

You're now good to go: make sure to connect your node, `deploy` and click on the button next to the inject node to see it working!

The complete flow can be found here: [Text To Speech on Bluemix lab flow using an URL](s2t_bluemix_url_flow.json)

---


The extended flow can be found here: [Extended Text To Speech lab flow ](s2t_flow_extended.json)
The flow in Node-Red in Bluemix can be found here: [Text To Speech lab flow for Bluemix](s2t_flow_bluemix.json)
