# Deep Linking In React Native.

## npx react-native@0.71.10 init DeepLinking --version 0.71.10

### Step 1. android/app/src/main/AndroidManifest.xml

```
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="demoapp" />
</intent-filter>
```

### Step 2. Add libraries

yarn add @react-navigation/native react-native-screens react-native-safe-area-context @react-navigation/native-stack @react-navigation/material-bottom-tabs react-native-paper react-native-vector-icons @react-native-masked-view/masked-view

### Step 3. App.tsx

```
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack'
import { createMaterialBottomTabNavigator } from '@react-navigation/material-bottom-tabs';
import HomeScreen from './screens/HomeScreen';
import ProfileScreen from './screens/ProfileScreen';
import FavScreen from './screens/FavScreen';
import Settings from './screens/Settings';
import { Image, StyleSheet, ActivityIndicator } from 'react-native';
//  import Icon from 'react-native-vector-icons/Ionicons'

const Tab = createMaterialBottomTabNavigator();

const Stack = createNativeStackNavigator();

const linking = {
  prefixes: ['demoapp://'],
  config: {
    screens: {
      HomeScreen: 'homescreen',
      FavouriteScreen: 'favscreen',
      ProfileScreen: {
        screens: {
          Profile: {
            path: 'profilescreen/:user/',
          },
        },
      },
      SettingsScreen: 'settingsscreen',
    },
  },
};

const App = () => (
  <NavigationContainer linking={linking}>
    <Tab.Navigator
      initialRouteName="Home"
      activeColor="#fff"
      headerShown={true}
      screenOptions={{
        headerStyle: {
          backgroundColor: '#009387',
        },
        headerTintColor: '#fff',
        headerTitleStyle: {
          fontWeight: 'bold',
        },
      }}
    >

      <Tab.Screen
        name="HomeScreen"
        component={HomeStackScreen}
        options={{
          title: 'Home',
          tabBarLabel: 'Home',
          tabBarColor: '#009387',
          tabBarIcon: ({ color }) => (
            <Image style={styles.image} source={{
              uri: 'https://logos.flamingtext.com/City-Logos/Todo-Logo.png',
            }} />
          ),
        }}
      />
      <Tab.Screen
        name="FavouriteScreen"
        component={FavStackScreen}
        options={{
          tabBarLabel: 'Favourite',
          tabBarColor: '#009387',
          tabBarIcon: ({ color }) => (
            <Image style={styles.image} source={{
              uri: 'https://logos.flamingtext.com/City-Logos/Todo-Logo.png',
            }} />
          ),
        }}
      />
      <Tab.Screen
        name="ProfileScreen"
        component={ProfileStackScreen}
        options={{
          tabBarLabel: 'Profile',
          tabBarColor: '#009387',
          tabBarIcon: ({ color }) => (
            <Image style={styles.image} source={{
              uri: 'https://logos.flamingtext.com/City-Logos/Todo-Logo.png',
            }} />
          ),
        }}
      />
      <Tab.Screen
        name="SettingsScreen"
        component={SettingsStackScreen}
        options={{
          tabBarLabel: 'Settings',
          tabBarColor: '#009387',
          tabBarIcon: ({ color }) => (
            <Image style={styles.image} source={{
              uri: 'https://logos.flamingtext.com/City-Logos/Todo-Logo.png',
            }} />
          ),
        }}
      />
    </Tab.Navigator>
  </NavigationContainer>
);


const HomeStackScreen = () => (
  <Stack.Navigator screenOptions={{
    headerStyle: {
      backgroundColor: '#009387',
    },
    headerTintColor: '#fff',
    headerTitleStyle: {
      fontWeight: 'bold',
    },
  }}>
    <Stack.Screen name="Home" component={HomeScreen} />
  </Stack.Navigator>
);

const FavStackScreen = () => (
  <Stack.Navigator screenOptions={{
    headerStyle: {
      backgroundColor: '#009387',
    },
    headerTintColor: '#fff',
    headerTitleStyle: {
      fontWeight: 'bold',
    },
  }}>
    <Stack.Screen name="Favourite" component={FavScreen} />
  </Stack.Navigator>
);

const ProfileStackScreen = () => (
  <Stack.Navigator screenOptions={{
    headerStyle: {
      backgroundColor: '#009387',
    },
    headerTintColor: '#fff',
    headerTitleStyle: {
      fontWeight: 'bold',
    },
  }}>
    <Stack.Screen name="Profile" component={ProfileScreen} />
  </Stack.Navigator>
);

const SettingsStackScreen = () => (
  <Stack.Navigator screenOptions={{
    headerStyle: {
      backgroundColor: '#009387',
    },
    headerTintColor: '#fff',
    headerTitleStyle: {
      fontWeight: 'bold',
    },
  }}>
    <Stack.Screen name="Settings" component={Settings} />
  </Stack.Navigator>
);

export default App;

const styles = StyleSheet.create({
  image: {
    flex: 1,
    width: 30,
    height: 30,
    resizeMode: 'contain',
  },
});
```

### Step 4. screens/HomeScreen.js

```
import React from 'react'
import {View, Text, StyleSheet} from 'react-native'

const HomeScreen = () => {
    return(
        <View style={styles.container}>
            <Text style={styles.title}>Welcome to React Native {'\n'} Deep Linking Tutorial</Text>
              
        </View>
    );
};

export default HomeScreen;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
    },
    title: {
    fontSize: 24,
    color: '#800000',
    textAlign: 'center',
    fontWeight: 'bold',
  },
  textDescription: {
    fontSize: 14,
    fontWeight: 'bold',
  },
});
```

### Step 5. screens/FavScreen.js

```
import React from 'react'
import {View, Text, Button, StyleSheet, Linking} from 'react-native'

const FavScreen = () => {

    const url_settings = 'demoapp://profilescreen/Smith';
    return(
        <View style={styles.container}>
            <Text style={styles.title}>Favourite Screen</Text>
            <Button
            title="Click Here"
            onPress={() => Linking.openURL(url_settings)}
            />
        </View>
    );
};

export default FavScreen;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
    },

    title: {
    fontSize: 24,
    color: '#800000',
    textAlign: 'center',
    fontWeight: 'bold',
  }, 
});
```

### Step 6. screens/ProfileScreen.js

```
import React from 'react'
import {View, Text, Button, StyleSheet} from 'react-native'

const ProfileScreen = ({route}) => {
    const {user} = route.params;

    return(
        <View style={styles.container}>
       <Text style={styles.title}>
        My name is {user}
       </Text>
        </View>
    );
};

export default ProfileScreen;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
    },
    title: {
    fontSize: 24,
    color: '#800000',
    textAlign: 'center',
    fontWeight: 'bold',
  }, 
});
```

### Step 7. screens/Settings.js

```
import React from 'react'
import {View, Text, Button, StyleSheet, Linking} from 'react-native'

const Settings = () => {
        const url_fav = 'demoapp://favscreen';
    return(
        <View style={styles.container}>
            <Text style={styles.title}>Settings Screen</Text>
            <Button
            title="Click Here"
            onPress={() => Linking.openURL(url_fav)}
            />
        </View>
    );
};

export default Settings;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
    },

    title: {
    fontSize: 24,
    color: '#800000',
    textAlign: 'center',
    fontWeight: 'bold',
  }, 
});
```
