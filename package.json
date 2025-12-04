import React, { useState, useEffect } from 'react';
import { View, Text, FlatList, TextInput, Button, Image, ActivityIndicator, Alert, StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const Tab = createBottomTabNavigator();

// ---------- FEED TAB ----------
function FeedScreen() {
  const posts = [
    { id: '1', text: 'Welcome to the Feed!' },
    { id: '2', text: 'React Native is fun!' },
    { id: '3', text: 'This is a random post example.' },
  ];

  return (
    <View style={styles.container}>
      <FlatList
        data={posts}
        keyExtractor={item => item.id}
        renderItem={({ item }) => <View style={styles.card}><Text>{item.text}</Text></View>}
      />
    </View>
  );
}

// ---------- DESCRIPTION TAB ----------
function DescriptionScreen() {
  const [imageData, setImageData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  const fetchImage = async () => {
    setLoading(true);
    setError(null);
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/photos/1');
      if (!res.ok) throw new Error('API Error');
      const data = await res.json();
      setImageData(data);
    } catch (err) {
      setError('Failed to fetch image');
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => { fetchImage(); }, []);

  return (
    <View style={styles.container}>
      {loading && <ActivityIndicator size="large" />}
      {error && <View><Text>{error}</Text><Button title="Retry" onPress={fetchImage} /></View>}
      {imageData && !loading && (
        <View style={{ gap: 10 }}>
          <Image source={{ uri: imageData.url }} style={styles.img} />
          <Text style={{ fontWeight: 'bold' }}>{imageData.title}</Text>
          <Button title="Load Again" onPress={fetchImage} />
        </View>
      )}
    </View>
  );
}

// ---------- PROFILE TAB ----------
function ProfileScreen() {
  const [name, setName] = useState('');
  const [regNo, setRegNo] = useState('');

  const saveInfo = () => {
    if (!name || !regNo) {
      Alert.alert('Please fill all fields');
    } else {
      Alert.alert('Saved!', `Name: ${name}\nRegistration No: ${regNo}`);
    }
  };

  return (
    <View style={styles.container}>
      <Text>Name:</Text>
      <TextInput style={styles.input} placeholder="Enter Name" value={name} onChangeText={setName} />
      <Text>Registration Number:</Text>
      <TextInput style={styles.input} placeholder="Enter Registration No" value={regNo} onChangeText={setRegNo} />
      <Button title="Save" onPress={saveInfo} />
    </View>
  );
}

// ---------- MAIN APP ----------
export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Feed" component={FeedScreen} />
        <Tab.Screen name="Description" component={DescriptionScreen} />
        <Tab.Screen name="Profile" component={ProfileScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}

// ---------- STYLES ----------
const styles = StyleSheet.create({
  container: { flex: 1, padding: 20 },
  card: { backgroundColor: '#fff', padding: 15, marginBottom: 10, borderRadius: 8, elevation: 3 },
  img: { width: '100%', height: 250, borderRadius: 8 },
  input: { borderWidth: 1, borderColor: '#ccc', padding: 8, marginBottom: 10, borderRadius: 6 },
});
