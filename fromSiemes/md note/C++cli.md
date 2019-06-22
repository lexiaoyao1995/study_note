c++ cli  

~~~c++
// CliDll.h

#pragma once

using namespace System;

namespace CliDll {

	class MapItem {
	public:
		int number;
		MapItem(int n) {
			number = n;
		}
	};

	class Democ {
	public:
		int getInt(int index) {
			return map[index]->number;
		}
		std::map<int, MapItem*> map;

		int flag = 1111;
	};

	public ref class Demo {
	public:
		Democ* a;
		Demo() {
			a = new Democ();
		}
		void say() {
			Console::WriteLine(L"Hello World");
		};

		Int32 getInt(Int32 index) {
			return a->getInt(index);
		}

		void insert(Int32 index , Int32 value) {
			MapItem *item = new MapItem(value);
			a->map[index] = item;
;
		}
	};

	public ref class Test {
	public:
		IOController *controller;
		Int32 m_iStartUpTime;
		
		inline void setm_iStartUpTime(Int32 m_iStartUpTime) {
			this->m_iStartUpTime = m_iStartUpTime;
		};

		void flush();
		
	};
}


~~~

