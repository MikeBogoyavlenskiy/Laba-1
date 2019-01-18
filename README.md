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
