[mongodb](http://www.mongodb.org) driver for delphi and freepascal. [Synapse](http://synapse.ararat.cz/) (blocking TCP Socket) is used for compatibility with freepascal.

**MOVED** the code repository is moved to http://github.com/pebbie/pebongo

### Current ###
  * JSON Parser
  * BSON I/O (**done**)
  * Wire Protocol Implementation (**in progress**)

## TODO ##
_ordered by priority_
  * create test code and code examples (always)
  1. implement mongodb protocol (**in progress**)
  1. create tool to convert BSON-JSON and vice versa (**BSON->JSON ok**)
  1. create documentation (tutorial, reference)
  1. create db navigator app

### Code Example ###
```
//example #2 on bsonspec.org
var
  bson              : TBSONDocument;
  item              : TBSONArrayItem;
begin
  bson := TBSONDocument.Create;
  item := TBSONArrayItem.Create;
  item.Items[0] := TBSONStringItem.Create( 'awesome' );
  item.Items[1] := TBSONDoubleItem.Create( 5.05 );
  item.Items[2] := TBSONIntItem.Create( 1986 );
  bson.Values['BSON'] := item;
  bson.SaveToFile( ExtractFilePath( Application.ExeName ) + 'hello.bson' );
  bson.Free;
```

```
//preliminary driver interface
var
  mongo             : TMongoConnection;
  coll              : TMongoCollection;
  cursor            : TMongoCursor;
  i                 : integer;
begin
  mongo := TMongoConnection.Create;
  memo1.lines.add( booltostr( mongo.Connected, true ) );
  mongo.GetDatabase( 'tesdb' );
  coll := mongo.GetCollection( 'things' );
  cursor := coll.find( );

  memo1.lines.add( inttostr( cursor.Count ) );
  for i := 0 to cursor.Count - 1 do
    memo1.lines.add( cursor.Result[i].ToString );//print as JSON

  cursor.Free;
  coll.Free;
  mongo.Free;
end;
```
