# codeRider
simple website<br>
Author-Saurabh

//Todo List 

import { View, Text, TextInput, TouchableOpacity, FlatList, StyleSheet } from 'react-native'
import React, { useState } from 'react'
export default function TodoList() {
    const [item, setItem] = useState("");
    const [itemData, setItemData] = useState([]);
    const [editText,setEditText] =useState(null)

    const addItems = ()=>{
        if(item.trim()){
            if(editText !==null){
                const newDataAdd = [...itemData]
                newDataAdd[editText] = item
                setItemData(newDataAdd)
                setEditText(null)
            }else{

                setItemData([...itemData,item])
            }
            setItem("")
        
        }
    }
    const deleteItem = (ind:number)=>{
        const deletes = itemData.filter((_: any,id: number)=>id!=ind)
        setItemData(deletes)
    }
    const editItem =(ind:number)=>{
     setItem(itemData[ind])
     setEditText(ind)
    }
    return (
        <View style={styles.container}>
            <Text style={styles.title}>TodoList</Text>
            <TextInput
                style={styles.input}
                value={item}
                onChangeText={setItem}
                placeholder="Enter item"
            />
            <TouchableOpacity style={styles.button} onPress={addItems}>
                <Text style={styles.buttonText}>Add</Text>
            </TouchableOpacity>
            <FlatList
                style={styles.list}
                data={itemData}
                keyExtractor={(item: string, index: { toString: () => void; }) => index.toString()}
                renderItem={({ item,index }) => (
                    <View style={styles.item}>
                        <Text style={styles.itemText}>{item}</Text>
                        <TouchableOpacity onPress={()=>editItem(index)} style={styles.buttonDel}>
                            <Text style={styles.buttonTxt}>edit</Text>
                        </TouchableOpacity>
                        <TouchableOpacity onPress={()=>deleteItem(index)} style={styles.buttonDel}>
                            <Text style={styles.buttonTxt}>x</Text>
                        </TouchableOpacity>
                    </View>
                )}
            />
        </View>
    )
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        height:48,
        width:300,
        padding: 20,
        backgroundColor: '#fff',
    },
    title: {
        fontSize: 24,
        fontWeight: 'bold',
        marginBottom: 20,
        textAlign: 'center',
    },
    input: {
        borderWidth: 1,
        borderColor: '#ccc',
        padding: 10,
        borderRadius: 5,
        marginBottom: 10,
    },
    button: {
        backgroundColor: '#007bff',
        padding: 10,
        borderRadius: 5,
        alignItems: 'center',
        marginBottom: 20,
    },
    buttonText: {
        color: '#fff',
        fontSize: 16,
        fontWeight: 'bold',
    },
    list: {
        flex: 1,
        marginTop: 20,
    },
    item: {
        justifyContent:"space-around",
        padding: 15,
        borderBottomWidth: 1,
        borderBottomColor: '#ccc',
        flexDirection:"row"
    },
    itemText: {
        fontSize: 18,
        color: "#000",
    },
    buttonDel:{
      alignSelf:"center",
      backgroundColor:"#C70000",
      paddingHorizontal:6,
      paddingVertical:3,
      borderRadius:24,
    },
    buttonTxt:
    {color:"#fff",textAlign: 'center',}
});





///////////////////////////////////////////////////////////



//
