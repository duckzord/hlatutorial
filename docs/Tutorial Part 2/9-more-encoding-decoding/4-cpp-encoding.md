---
sidebar_position: 4
---

# C++ Encoding Helpers

These examples will show you how to encode and decode all the different datatypes. Each example will have one section for encoding and another for decoding. The encoding code would be placed where you are sending updates while the decoding code would probably be placed in your callbacks for reflecting attribute values or receiving interactions.

Before going into the examples take a look at the example code below that shows a typical way to iterate over attributes in the reflect attribute values callback or parameters in the receive interaction callback, this also explains where the value-variable comes from in all the other examples


```cpp
for (AttributeHandleValueMap::const_iterator i = theAttributeValues.begin();
       i != theAttributeValues.end(); ++i) {

AttributeHandle const & handle = i->first;
VariableLengthData const & value = i->second;

   if (handle == <an attribute handle>) {
      // Place code here for decoding the attribute value and process the data		
   }
}
```

#### Simple datatype
Simple datatypes are very simple to work with, just create the datatype you need (remember that all simple datatypes has a basic datatype representation). The value of the datatype can be given when creating it or using the set-function.

```cpp
// Encoding a simple datatype
AttributeHandleValueMap _attrHandleValueMap;

HLAinteger32BE octaneRating(50); // sets the value to 50
_attrHandleValueMap[_octaneRatingAttribute] = octaneRating.encode();

_rtiAmbassador->updateAttributeValues(carHandle, _attrHandleValueMap, VariableLengthData());

	
// Decoding a simple datatype
HLAinteger32BE octaneRating;

try {
   // value is from the theAttributeValues parameter in reflectAttributeValues
   octaneRating.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}


Enumerated datatype
Enumerated datatypes are also very simple to work with, again create the data type that you need.

// Encoding an enumerated datatype
AttributeHandleValueMap _attrHandleValueMap;

HLAinteger32BE dieselType(2); // sets the value to 2
_attrHandleValueMap[_dieselTypeAttribute] = dieselType.encode();

_rtiAmbassador->updateAttributeValues(carHandle, _attrHandleValueMap, VariableLengthData());	


// Decoding a simple datatype
HLAinteger32BE dieselType;

try {
   // value is from the theAttributeValues parameter in reflectAttributeValues
   dieselType.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}
```



#### Fixed array

When creating a fixed array you have to specify the type that will be contained in the array. This is done by the prototype in the example below. When accessing elements in a fixed array it has to be casted to the correct type, see the for-loop in the example below that prints the content of the array.

If you are working with a fixed array with a small number of elements you can avoid having to use casting by setting elements into the array with the setElementPointer-function manually when decoding, but for larger arrays that can quickly become too many variables to be convenient.

```cpp
// Encoding a fixed array
AttributeHandleValueMap _attrHandleValueMap;

HLAunicodeString prototype;
HLAfixedArray leaderBoardArray(prototype, 3);

leaderBoardArray.set(0, HLAunicodeString(L"CarName1"));
leaderBoardArray.set(1, HLAunicodeString(L"CarName2"));
leaderBoardArray.set(2, HLAunicodeString(L"CarName3"));

_attrHandleValueMap[_top3Attribute] = leaderBoardArray.encode();

_rtiAmbassador->updateAttributeValues(leaderBoardHandle, _attrHandleValueMap,
                                                                           VariableLengthData());

// Decoding a fixed array
HLAunicodeString prototype;
HLAfixedArray leaderBoardArray(prototype, 3);

try {
// value is from the theAttributeValues parameter in reflectAttributeValues
   leaderBoardArray.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}

// Printing the content of the array, notice the usage of the dynamic_cast
for (size_t i = 0; i < leaderBoardArray.size(); i++) {
   wcout << dynamic_cast<const HLAunicodeString &>(leaderBoardArray[i]).get() << endl;
}
```

#### Variable Array

When creating a variable array you have to specify the type that will be contained in the array. This is done by the prototype in the example below. When accessing elements in a variable array it has to be casted to the correct type, see the for-loop in the example below that prints the content of the array.

```cpp
// Encoding a variable array
AttributeHandleValueMap _attrHandleValueMap;

HLAunicodeString prototype;
HLAvariableArray carNameArray(prototype);

carNameArray.addElement(HLAunicodeString(L"CarName1"));
carNameArray.addElement(HLAunicodeString(L"CarName2"));
carNameArray.addElement(HLAunicodeString(L"CarName3"));
carNameArray.addElement(HLAunicodeString(L"CarName4"));

_attrHandleValueMap[_allCarsAttribute] = carNameArray.encode();

_rtiAmbassador->updateAttributeValues(leaderBoardHandle, _attrHandleValueMap,
                                                                           VariableLengthData());


// Decoding a variable array
HLAunicodeString prototype;
HLAvariableArray carNameArray(prototype);

try {
   // value is from the theAttributeValues parameter in reflectAttributeValues
   carNameArray.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}

// Printing the content of the array, notice the usage of the dynamic_cast
for (size_t i = 0; i < carNameArray.size(); i++) {
   wcout << dynamic_cast<const HLAunicodeString &>(carNameArray[i]).get() << endl;
}
```

Fixed Record
When working with fixed records it is convenient to keep the references to the items you put into the fixed record. The reason is that when using get methods to get values from the fixed record you will get a DataElement-type which has to be casted to the correct type. For example, in the example below, after decoding the fixed record the field values can be accessed directly in octaneRating and isLeaded.

``` cpp
// Encoding a fixed record
AttributeHandleValueMap _attrHandleValueMap;

HLAinteger32BE octaneRating(50);
HLAboolean isLeaded(false);

HLAfixedRecord gasolineRecord;

gasolineRecord.appendElement(octaneRating);
gasolineRecord.appendElement(isLeaded);

_attrHandleValueMap[_gasolineAttribute] = gasolineRecord.encode();

_rtiAmbassador->updateAttributeValues(carHandle, _attrHandleValueMap, VariableLengthData());


// Decoding a fixed record
HLAinteger32BE octaneRating;
HLAboolean isLeaded;

HLAfixedRecord gasolineRecord;

gasolineRecord.appendElementPointer(&octaneRating);
gasolineRecord.appendElementPointer(&isLeaded);

try {
   // value is from the theAttributeValues parameter in reflectAttributeValues
   gasolineRecord.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}
```



#### Variant Record
When working with variant records it is usually easiest to keep the references to the items you put into the variant record, just as for fixed records as described above. Note that when encoding the variant record you only have to create the alternative you want to encode, but when decoding all the possible variants has to be added to the variant record as you can’t know which variant will be used.

When decoding the variant array in the example below the alternatives are added to the variant array using the appendElementPointer-function. This means that when decoding the variant record the content can be accessed directly in those variables. This is not true for the discriminant, the fuelStatusDiscriminant variable will not have the correct value after the decode-function. It can be convenient to set that variable to the correct value as shown in the last line of this example.

```cpp
// Encoding a variant record
AttributeHandleValueMap carAttributes =
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE(50);
HLAboolean isLeaded = _encoderFactory.createHLAboolean(false);

HLAfixedRecord gasolineRecord = _encoderFactory.createHLAfixedRecord();  
gasolineRecord.add(octaneRating);
gasolineRecord.add(isLeaded);

HLAinteger32BE fuelStatusDiscriminant = _encoderFactory.createHLAinteger32BE(1); // create discriminant
HLAvariantRecord<HLAinteger32BE> fuelStatusVariantRec =
      _encoderFactory.createHLAvariantRecord(fuelStatusDiscriminant);  // create the variant record
fuelStatusVariantRec.setVariant(fuelStatusDiscriminant, gasolineRecord);  

carAttributes.put(_fuelStatusAttribute, fuelStatusVariantRec.toByteArray());

_rtiAmbassador.updateAttributeValues(carHandle, carAttributes, null);	


// Decoding a variant record
HLAinteger32BE octaneRating;
HLAboolean isLeaded;

HLAfixedRecord gasolineRecord;

gasolineRecord.appendElementPointer(&octaneRating);
gasolineRecord.appendElementPointer(&isLeaded);

HLAinteger32BE dieselType;
HLAinteger32BE cetaneNumber;
					
HLAfixedRecord dieselRecord;

dieselRecord.appendElementPointer(&dieselType);
dieselRecord.appendElementPointer(&cetaneNumber);

HLAinteger32BE ethanolFuelMixture;

HLAinteger32BE naturalGasType;

HLAinteger32BE fuelStatusDiscriminant;
HLAvariantRecord fuelStatusVariantRec(fuelStatusDiscriminant);				

HLAinteger32BE gasolineAlternative(1);
HLAinteger32BE dieselAlternative(2);
HLAinteger32BE ethanolAlternative(3);
HLAinteger32BE naturalGasAlternative(4);

fuelStatusVariantRec.addVariantPointer(gasolineAlternative, &gasolineRecord);
fuelStatusVariantRec.addVariantPointer(dieselAlternative, &dieselRecord);
fuelStatusVariantRec.addVariantPointer(ethanolAlternative, &ethanolFuelMixture);
fuelStatusVariantRec.addVariantPointer(naturalGasAlternative, &naturalGasType);
					
try {
   // value is from the theAttributeValues parameter in reflectAttributeValues
   fuelStatusVariantRec.decode(value);
} catch (EncoderException &e) {
   // Handle exception
}

fuelStatusDiscriminant.set(
   (dynamic_cast<const HLAinteger32BE &>(fuelStatusVariantRec.getDiscriminant()).get()));
```



