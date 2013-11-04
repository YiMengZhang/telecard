telecard
========
#include <iostream>
#include <Windows.h>
#include <conio.h>
#include <string>

using namespace std;

class PhoneCard {
  int password;

public:
  double balance;

  long connectNumber;

  double additoryFee;

  long cardNumber;

  bool connected;

  class phonecard:public PhoneCard 
  {
  public:
	phonecard  (long cn, int pw, double b, long conNumber, double addFee  )
    // 卡号、密码、剩余金额及接入号码的设置
    cardNumber = cn;
    password = pw;
    balance = b;
    connectNumber = conNumber;
    additoryFee = addFee;
  }

  void performConnect(long cn, int pw){
    cout<<"正在拨打 "<<connectNumber<<"..."<<endl;

    // 模拟等待时间 1 秒
    Sleep(1000);

    // 检查用户名和密码
    if(cn != cardNumber || pw != password) {
      cout<<"用户名/密码错误。"<<endl;
      return;
    }

    // 提示拨号
    cout<<"您的卡号: "<<cardNumber<<endl;
    cout<<"您的密码: "<<password<<"\n\n确认使用 (Y/N)？"<<endl;
    char choice;
    choice = _getch();

    if(choice == 'Y' || choice == 'y')
      performDial();
    else
      cout<<"您取消了拨号\n"<<endl;
  }

  double getBalance() {
    if(connected)
      return balance;
    else
      return 0;
  }

  virtual void performDial() {};
};

class Card_201 : public PhoneCard{

public:

  Card_201(long cn, int pw, double b):PhoneCard(cn, pw, b, 201, 0.03) {
  }

  bool deductBalance(double b) {
    // 判断余额是否足够
    if((balance-b-additoryFee) >= 0) {
      balance -= b + additoryFee;
      return true;
    } else
      return false;
  }

  void performDial() {
    {
      cout<<"201 卡正在拨号..."<<endl;

      // 模拟等待时间 1.5 秒
      Sleep(1500);

      if(deductBalance(0.3)) {
        cout<<"电话接通，开始计费"<<endl;

        // 连接状态
        connected = true;

        // 模拟等待时间 1 秒
        Sleep(1000);

        cout<<"通话结束，您的余额还有 "<<getBalance()<<" , 谢谢使用\n"<<endl;
      } else
        cout<<"您的余额不足，请充值，谢谢\n"<<endl;

      connected = false;
    }
  }                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
};

int  main()
{
            int cn;
			long pw;
			double balance;
			PhoneCard( cn,  pw,  balance);
			cout<<"please input your number cn="<<endl;
			cout<<"pleaseset your password pw="<<endl;
            cout<<"please input your balance="<<endl;
			cin>>cn;
			cin>>pw;
			cin>>balance;



            Card_201 card( cn, pw, balance);
			cout<<"please input your cardnumber cn=";
			cout<<"please input your password pw=";
			cin>>cn;
			cin>>pw;
			 

            while(true) {
              card.performConnect(cn, pw);

              cout<<"继续使用本系统吗 (Y/n) ?"<<endl;
              int choice = 0;
              choice = _getch();

              if(choice == 'Y' || choice == 'y') {
                cout<<"------------------------------------------"<<endl;
                continue;
              } else {
                cout<<"谢谢使用，再见！\n\n"<<endl;
                break;
              }
            } 
    return 0;
} 
        
  
 
