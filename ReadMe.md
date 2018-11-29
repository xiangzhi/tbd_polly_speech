# success_polly_speech
License - MIT  
Maintainer - zhi.tan@ri.cmu.edu  

A ROS wrapper for Amazon Polly Text-to-Speech service. We also cache locally each soundfile, so if you ever repeat the same sentence with the same voice, a local copy of the audio will be used instead of sythesizing it again.

## Usage

### Running 
1. Make sure you have a AWS credentials file setup on the system. [Guide by AWS](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html). Make sure the account has AWS Polly Speech Enabled
2. launch the backend services
```
roslaunch success_polly_speech polly_speech.launch
```
3. You can access the service either through the Python API
```
from suicces_polly_speech import PollySpeech

ps = PollySpeech()

ps.speak("I am a good robot",voice_id='Joanna')
ps.speak("I am not a scary robot",voice_id='Joanna', block=False)
ps.wait()
ps.speak('Hello World. I will be interrupted',voice_id='Emma', block=False, cancel=True) 
ps.stopAll() #Interrupts the sentence and stop the voice command
```
OR directly calling the action server at the topic `success_polly_speech/speak` with the action `pollySpeechAction`.

### ROS Parameters
There are two ROS parameters in the launch file
* `no_audio`, true if you just want to simulate it and not actually running the code. 
* `polly_audio_storage_path`, the path to the location you want to store the audio and also the `masterlist.txt` which stores the coding from phrases/text to filename. the default is `PACKAGE_ROOT/audio_storage`

### Voices
A list of voice ID can be found here: https://docs.aws.amazon.com/polly/latest/dg/voicelist.html

## Past Contributors
- Joe Connolly - 07/2018