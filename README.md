# Laba-1
#include<string>
#include<iostream>
#include"Exception.hpp"
using namespace std;
class Note{
	string name;
	string surname;
	string phone;
	int date[3];
public:
	Note(const string& name = "", const string& surname = "", const string& phone = "", int day = 0, int month = 0, int year = 0);
	Note(const Note& note);
	~Note();
	//геттеры и сеттеры
	string& Name();
	string& Surname();
	string& Phone();
	int& Month();
	int& Day();
	int& Year();
	//операторы
	friend ostream& operator<<(ostream& out, const Note& note);
	friend istream& operator>>(istream& in, Note& note);
	Note& operator =(const Note& note);
};

//реализатор класса Note
#include "Note.h"//подключаем интерфес класса

Note::Note(const string& name, const string& surname, const string& phone, int day, int month, int year){//конструктор класса
  cout << "\nNote()";
  this->name = name;
  this->surname = surname;
  this->phone = phone;
  this->date[0] = day;
  this->date[1] = month;
  this->date[2] = year;
}
Note::Note(const Note& note){//конструктор копирования
  cout << "\nNote(Note)";
  this->name = note.name;
  this->surname = note.surname;
  this->phone = note.phone;
  this->date[0] = note.date[0];
  this->date[1] = note.date[1];
  this->date[2] = note.date[2];
}
Note::~Note(){//деструктор
	cout << "~Note()";
}
//геттеры и (сеттеры)
string& Note::Name(){
	return name;
}
string& Note::Surname(){
	return surname;
}
string& Note::Phone(){
	return phone;
}
int& Note::Month(){
	return date[1];
}
int& Note::Day(){
	return date[0];
}
int& Note::Year(){
	return date[2];
}
//операторы
ostream& operator<<(ostream& out, const Note& note){//перегрузка оператор вывода
	out << note.name << '\n' << note.surname << '\n' << note.phone << '\n' <<
		note.date[0] << '/' << note.date[1] << '/' << note.date[2];
	return out;
}
istream& operator>>(istream& in, Note& note){//перегрузка оператор ввода
	if(!(in >> note.name >> note.surname >> note.phone >> note.date[0] >> note.date[1] >> note.date[2])){
		throw Exception("Ошибка ввода");
	}
	return in;
}
Note& Note::operator =(const Note& note){//перегрузка оператор присваивания
  if(this == &note) return *this;
  this->name = note.name;
  this->surname = note.surname;
  this->phone = note.phone;
  this->date[0] = note.date[0];
  this->date[1] = note.date[1];
  this->date[2] = note.date[2];
  return *this;
}
#include "Note.h"

int main(){
	const int size = 8;//размер
	setlocale(LC_ALL, "");
	Note notes[size];//массив знаков
	int choice;
	while(true){
		 cout << "\n1. Считать\n2. Поиск\n3. Изменить\n4. Выход\n-> ";
		 cin >> choice;
		 if(choice == 1){
			 cout << "Имя Фамилия Телефон DD MM YY\n";
			 try{
				 //считываем данные
				for(int i = 0; i < size; ++i){
				   cin >> notes[i];
				}
				/*Сортируем*/
				int j, n = size;
				do {
					int nn = 0;
					for (j = 1; j < n; ++j)
						if (notes[j-1].Day() > notes[j].Day() 
							&& notes[j-1].Month() > notes[j].Month()
							&& notes[j-1].Year() > notes[j].Year()) {
							Note temp = notes[j-1];
							notes[j-1] = notes[j];
							notes[j] = temp;
							nn = j;
						}
						n = nn;
				} while (n);
			 }
			 catch(const Exception& e){ // по константной ссылке
				cout << "\n" << e.what();
			 }
		 }
		 else if(choice == 2){
			 cout << "Введите номер телефона: ";
			 string phone;
			 cin >> phone;
			 int i;
			 for(i = 0; i < size; ++i){
				if(notes[i].Phone() == phone){
					cout << "\n" << notes[i];
				}
			 }
			 if(i > size){
				cout << "NOT FOUND";
			 }
		 }
		 else if(choice == 3){
			 int index;
			 do{
				cout << "Введите индекс: ";
				cin >> index;
			 } while(index < 0 || index >= 8);//защита от некорректного ввода
			 cout << "Имя Фамилия Телефон DD MM YY\n";
			 cin >> notes[index];
		 }
		 else if(choice == 4){
			 return 0;
		 }
	}
}
#pragma once//подключить 1 раз
#include <string>

class Exception{
private:
	std::string message;
public:
	explicit Exception(const std::string &message = "Exception");
	const std::string& what() const;
};
#include "Exception.hpp"

Exception::Exception(const std::string &message):message(message){}
const std::string& Exception::what() const { return message; }
