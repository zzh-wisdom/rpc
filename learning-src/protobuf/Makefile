# See README.txt.

.PHONY: all cpp

all: cpp

cpp:    add_person_cpp    list_people_cpp

clean:
	rm -f add_person_cpp list_people_cpp add_person_java list_people_java add_person_python list_people_python
	rm -f javac_middleman AddPerson*.class ListPeople*.class com/example/tutorial/*.class
	rm -f protoc_middleman addressbook.pb.cc addressbook.pb.h addressbook_pb2.py com/example/tutorial/AddressBookProtos.java
	rm -f *.pyc
	rm -f protoc_middleman_go tutorial/*.pb.go add_person_go list_people_go
	rm -f protoc_middleman_dart dart_tutorial/*.pb*.dart
	rmdir dart_tutorial 2>/dev/null || true
	rmdir tutorial 2>/dev/null || true
	rmdir com/example/tutorial 2>/dev/null || true
	rmdir com/example 2>/dev/null || true
	rmdir com 2>/dev/null || true

protoc_middleman: addressbook.proto
	protoc $$PROTO_PATH --cpp_out=. addressbook.proto
	@touch protoc_middleman  # 辅助文件？

add_person_cpp: add_person.cc protoc_middleman
	pkg-config --cflags protobuf  # fails if protobuf is not installed
	c++ -std=c++11 add_person.cc addressbook.pb.cc -o add_person_cpp `pkg-config --cflags --libs protobuf`

list_people_cpp: list_people.cc protoc_middleman
	pkg-config --cflags protobuf  # fails if protobuf is not installed
	c++ -std=c++11 list_people.cc addressbook.pb.cc -o list_people_cpp `pkg-config --cflags --libs protobuf`