Change to: 
```
buildToolsVersion = findProperty('android.buildToolsVersion') ?: '33.0.1'
```
```
build.gradle: api "androidx.core:core-ktx:1.10.1"
```

I needed to install watchman with brew as others have done here, however I also needed to update the React Native Xcode build script with this line: export PATH=/opt/homebrew/bin:$PATH so xCode could find watchman in my M1 MacBook Pro.

React Native Xcode build script location: ./node_modules/react-native/scripts/react-native-xcode.sh


inside /android  run :
```
chmod +x gradlew
```
```
./gradlew build
```
```     
npm i
```
Then   
```
 yarn run android
```


#### week 6
in screen/First , remove import Checkbox, and run 
```
npm i expo-checkbox -f
```
Then change import:   
```
import CheckBox from 'expo-checkbox';

```
