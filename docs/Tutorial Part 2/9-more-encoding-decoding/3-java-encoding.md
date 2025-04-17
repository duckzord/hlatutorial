---
sidebar_position: 3
---

# Java Encoding Helpers

These examples will show you how to encode and decode all the different datatypes. Each example will have one section for encoding and another for decoding. The encoding code would be placed where you are sending updates while the decoding code would probably be placed in your callbacks for reflecting attribute values or receiving interactions.

#### Encoder Factory
All examples below will make use of an encoder factory which is obtained as shown below.

```java
RtiFactory rtiFactory = RtiFactoryFactory.getRtiFactory();
EncoderFactory _encoderFactory = rtiFactory.getEncoderFactory();
```




#### Simple datatype

Simple datatypes are very simple to work with, just use the encoder factory to create the datatype you need (remember that all simple datatypes has a basic datatype representation). The value of the datatype can be given when creating it or using the setValue method.

```java
// Encoding a simple datatype
AttributeHandleValueMap carAttributes  =
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE(50);  // sets the value to 50

carAttributes.put(_octaneRatingAttribute, octaneRating.toByteArray());
_rtiAmbassador.updateAttributeValues(carHandle, carAttributes, null);

	
// Decoding a simple datatype
HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE();
try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   octaneRating.decode(theAttributes.get(_octaneRatingAttribute));
} catch (DecoderException e) {
   // Handle exception
}
```

#### Enumerated datatype
Enumerated datatypes are also very simple to work with, again just use the encoder factory to create the data type that you need.

```java
// Encoding an enumerated datatype
AttributeHandleValueMap carAttributes =
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAinteger32BE dieselType = _encoderFactory.createHLAinteger32BE(2);  // sets the value to 2

carAttributes.put(_dieselTypeAttribute, dieselType.toByteArray());
_rtiAmbassador.updateAttributeValues(carHandle, carAttributes, null);


// Decoding a simple datatype
HLAinteger32BE dieselType = _encoderFactory.createHLAinteger32BE();
try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   dieselType.decode(theAttributes.get(_dieselTypeAttribute));
} catch (DecoderException e) {
   // Handle exception
}
```

#### Fixed array

When creating a fixed array you can specify the data element factory to use. The array will use this factory to create empty elements in the array. It is possible to avoid using a factory by specifying all the elements when creating the fixed array.

```java
// Data element factory
// Usually defined once elsewhere in the code
DataElementFactory<HLAunicodeString> _unicodeStringFactory =
      new DataElementFactory<HLAunicodeString>()
{
   public HLAunicodeString createElement(int index)
   {
      return _encoderFactory.createHLAunicodeString();
   }
};

// Encoding a fixed array
AttributeHandleValueMap leaderBoardsAttributes = 
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAfixedArray<HLAunicodeString> leaderBoardArray = 
      _encoderFactory.createHLAfixedArray(_unicodeStringFactory, 3);  // creates the fixed array

leaderBoardArray.get(0).setValue("CarName1"); // set the element values
leaderBoardArray.get(1).setValue("CarName2");
leaderBoardArray.get(2).setValue("CarName3");

leaderBoardsAttributes.put(_top3Attribute, leaderBoardArray.toByteArray());
_rtiAmbassador.updateAttributeValues(leaderBoardHandle, leaderBoardsAttributes, null);	


// Decoding a fixed array
HLAfixedArray<HLAunicodeString> leaderBoardArray = 
      _encoderFactory.createHLAfixedArray(_unicodeStringFactory, 3);

try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   leaderBoardArray.decode(theAttributes.get(_top3Attribute));
} catch (DecoderException e) {
   // Handle exception
}
```

#### Variable Array
When creating a variable array the data element factory is required.

```java
// Data element factory
// Usually defined once elsewhere in the code
DataElementFactory<HLAunicodeString> _unicodeStringFactory =
      new DataElementFactory<HLAunicodeString>()
{
   public HLAunicodeString createElement(int index)
   {
      return _encoderFactory.createHLAunicodeString();
   }
};


// Encoding a variable array
AttributeHandleValueMap leaderBoardsAttributes = 
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAvariableArray<HLAunicodeString> carNameArray =
      _encoderFactory.createHLAvariableArray(_unicodeStringFactory);  // creates the variable array

carNameArray.addElement(_encoderFactory.createHLAunicodeString("CarName1"));
carNameArray.addElement(_encoderFactory.createHLAunicodeString("CarName2"));
carNameArray.addElement(_encoderFactory.createHLAunicodeString("CarName3"));
carNameArray.addElement(_encoderFactory.createHLAunicodeString("CarName4"));

leaderBoardsAttributes.put(_allCarsAttribute, carNameArray.toByteArray());

_rtiAmbassador.updateAttributeValues(leaderBoardHandle, leaderBoardsAttributes, null);	


// Decoding a variable array
HLAvariableArray<HLAunicodeString> carNameArray =
      _encoderFactory.createHLAvariableArray(_unicodeStringFactory);

try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   carNameArray.decode(theAttributes.get(_allCarsAttribute));
} catch (DecoderException e) {
   // Handle exception
}
```

#### Fixed Record

When working with fixed records it is convenient to keep the references to the items you put into the fixed record. The reason is that when using get methods to get values from the fixed record you will get a DataElement-type which has to be casted to the correct type. For example, in the example below, after decoding the fixed record the field values can be accessed directly in octaneRating and isLeaded.

```java
// Encoding a fixed record
AttributeHandleValueMap carAttributes =
      _rtiAmbassador.getAttributeHandleValueMapFactory().create(1);

HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE(50);
HLAboolean isLeaded = _encoderFactory.createHLAboolean(false);

HLAfixedRecord gasolineRecord = _encoderFactory.createHLAfixedRecord();  // create the fixed record
gasolineRecord.add(octaneRating);
gasolineRecord.add(isLeaded);

carAttributes.put(_gasolineAttribute, gasolineRecord.toByteArray());

_rtiAmbassador.updateAttributeValues(carHandle, carAttributes, null);	


// Decoding a fixed record

HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE();
HLAboolean isLeaded = _encoderFactory.createHLAboolean();

HLAfixedRecord gasolineRecord = _encoderFactory.createHLAfixedRecord();
gasolineRecord.add(octaneRating);
gasolineRecord.add(isLeaded);

try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   gasolineRecord.decode(theAttributes.get(_gasolineAttribute));
} catch (DecoderException e) {
   // Handle exception
}
```

#### Variant Record
When working with variant records it is usually easiest to keep the references to the items you put into the variant record, just as for fixed records as described above. Note that when encoding the variant record you only have to create the alternative you want to encode, but when decoding all the possible variants has to be added to the variant record as you can’t know which variant will be used.

```java
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
HLAinteger32BE octaneRating = _encoderFactory.createHLAinteger32BE();
HLAboolean isLeaded = _encoderFactory.createHLAboolean();

HLAfixedRecord gasolineRecord = _encoderFactory.createHLAfixedRecord();
gasolineRecord.add(octaneRating);
gasolineRecord.add(isLeaded);

HLAinteger32BE dieselType = _encoderFactory.createHLAinteger32BE();
HLAinteger32BE cetaneNumber = _encoderFactory.createHLAinteger32BE();

HLAfixedRecord dieselRecord = _encoderFactory.createHLAfixedRecord();
dieselRecord.add(dieselType);
dieselRecord.add(cetaneNumber);

HLAinteger32BE ethanolFuelMixture = _encoderFactory.createHLAinteger32BE();

HLAinteger32BE naturalGasType = _encoderFactory.createHLAinteger32BE();

HLAinteger32BE fuelStatusDiscriminant = _encoderFactory.createHLAinteger32BE();
HLAvariantRecord<HLAinteger32BE> fuelStatusVariantRec =
      _encoderFactory.createHLAvariantRecord(fuelStatusDiscriminant);

HLAinteger32BE gasolineAlternative = _encoderFactory.createHLAinteger32BE(1);
HLAinteger32BE dieselAlternative = _encoderFactory.createHLAinteger32BE(2);
HLAinteger32BE ethanolAlternative = _encoderFactory.createHLAinteger32BE(3);
HLAinteger32BE naturalGasAlternative = _encoderFactory.createHLAinteger32BE(4);

fuelStatusVariantRec.setVariant(gasolineAlternative, gasolineRecord);
fuelStatusVariantRec.setVariant(dieselAlternative, dieselRecord);
fuelStatusVariantRec.setVariant(ethanolAlternative, ethanolFuelMixture);
fuelStatusVariantRec.setVariant(naturalGasAlternative, naturalGasType);

try {
   // theAttributes is a parameter in the reflectAttributeValues callback
   fuelStatusVariantRec.decode(theAttributes.get(_fuelStatusAttribute));
} catch (DecoderException e) {
   // Handle exception
}
```

