```C++
// 魔兽一：备战.cpp: 定义控制台应用程序的入口点。
//
#include "stdafx.h"
#include<iostream>
#include<string.h>
#include<string>
#include<cstring>
#include<iomanip>
using namespace std;
static int Time = 0;
static int  dragon_life, ninja_life, iceman_life, lion_life, wolf_life;
class Headquarter
{
public:
	//static int  dragon_life, ninja_life, iceman_life, lion_life, wolf_life;
	void set_life()
	{
		cin >> dragon_life >> ninja_life >> iceman_life >> lion_life >> wolf_life;
	}
};
class Red_Headquarter :public Headquarter
{
public:
	int Life_yuan;
	int num = 0;
	int jumps = 0;
	enum sodiers { iceman, lion, wolf, ninja, dragon };
	string Name[5] = { "iceman", "lion", "wolf", "ninja", "dragon" };
	int life_[5] = { 0 };
	int status[5] = { 0 };
	int NumbersOfSodiers[5] = { 0 };
	Red_Headquarter() { set_life(); }
	bool check_stop();
	bool jump(int a);
	void produce();
	Red_Headquarter(int a) :Life_yuan(a) { set_life(); };
	void set_life();
};

class Blue_Headquarter :public Headquarter
{
public:
	int Life_yuan;
	int num = 0;
	int jumps = 0;
	enum sodiers { lion, dragon, ninja, iceman, wolf };
	string Name[5] = { "lion", "dragon", "ninja", "iceman", "wolf" };
	int life_[5] = { 0 };
	int status[5] = { 0 };
	int NumbersOfSodiers[5] = { 0 };
	Blue_Headquarter() { set_life(); }
	bool check_stop();
	bool jump(int a);
	void produce();
	Blue_Headquarter(int a) :Life_yuan(a) { set_life(); };
	void set_life();
};
////////////////////////////////////////////////////以下为红方
void Red_Headquarter::set_life()
{
	life_[lion] = lion_life;
	life_[wolf] = wolf_life;
	life_[iceman] = iceman_life;
	life_[dragon] = dragon_life;
	life_[ninja] = ninja_life;
}
bool Red_Headquarter::check_stop()
{
	for (int i = 0; i < 5; i++)
	{
		if (Life_yuan < life_[i])
			status[i] = 1;
	}
	if (status[iceman] && status[lion] && status[wolf] && status[ninja] && status[dragon])
		return true;
	else return false;
}
bool Red_Headquarter::jump(int a)
{
	if (status[a])
	{
		jumps++;
		return true;
	}
	else return false;
}
void Red_Headquarter::produce()
{

	int temp = (num+jumps) % 5;//temp是角标
	while (jump(temp))
	{
		temp = (temp + 1) % 5;
	}
	NumbersOfSodiers[temp]++;
	num++;
	cout << setw(3) << setfill('0') << Time << ' ' << "red " << Name[temp] << ' ' << num << " born with strength " << life_[temp]<< ',' << NumbersOfSodiers[temp] << ' ' << Name[temp] << " in red headquarter" << endl;
	Life_yuan -= life_[temp];
}
/////////////////////////////////////////////////// 以上为红方
/////////////////////////////////////////////////// 以下为蓝方
void Blue_Headquarter::set_life()
{
	life_[lion] = lion_life;
	life_[wolf] = wolf_life;
	life_[iceman] = iceman_life;
	life_[dragon] = dragon_life;
	life_[ninja] = ninja_life;
}
bool Blue_Headquarter::check_stop()
{
	for (int i = 0; i < 5; i++)
	{
		if (Life_yuan < life_[i])
			status[i] = 1;
	}
	if (status[iceman] && status[lion] && status[wolf] && status[ninja] && status[dragon])
		return true;
	else return false;
}
bool Blue_Headquarter::jump(int a)
{
	if (status[a])
	{
		jumps++;
		return true;
	}
	else return false;
}
void Blue_Headquarter::produce()
{
	int temp = (num+jumps) % 5;//temp是角标
	while (jump(temp))
	{
		temp = (temp + 1) % 5;
	}
	NumbersOfSodiers[temp]++;
	num++;
	
	cout << setw(3) << setfill('0')<< Time << " " << "blue " << Name[temp] << " " << num << " born with strength " << life_[temp]<< ',' << NumbersOfSodiers[temp] << " " << Name[temp] << " in blue headquarter" << endl;
	Life_yuan -= life_[temp];
}
/////////////////////////////////////////////////// 以上为蓝方

int main()
{
	int Case;
	cin >> Case;
	int NO = Case;
	while (Case)
	{		
		
		int life_yuan;
		cin >> life_yuan;		
		Headquarter h;
		h.set_life();
		cout << "Case:" << NO-Case+1 << endl;
		Red_Headquarter red(life_yuan);
		Blue_Headquarter blue(life_yuan);
		bool red_can_produce = true;
		bool blue_can_produce = true;
		while (red_can_produce || blue_can_produce)
		{

			if (red.check_stop())
			{
				if (red_can_produce)
			
					cout << setw(3)<<setfill('0') <<Time << " " << "red headquarter stops making warriors" << endl;
				red_can_produce = false;
			}
			if (blue.check_stop())
			{
				if (blue_can_produce)
				
					cout << setw(3) << setfill('0') << Time << " " << "blue headquarter stops making warriors" << endl;
					blue_can_produce = false;
			}
			if (red_can_produce)
				red.produce();
			if (blue_can_produce)
				blue.produce();
			Time++;			
			
		}
		Case--;
		Time = 0;
	}
	system("pause");
	return 0;
}


```
