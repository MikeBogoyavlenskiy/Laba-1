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

