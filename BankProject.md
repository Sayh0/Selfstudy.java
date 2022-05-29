## Account
<br/>

```java
package BankProject;

public class Account {
	private String id;
	private String pwd;
	private int money;
	
	public Account(String id2, String pwd2, int money2) {
		id = id2;
		pwd = pwd2;
		money = money2;
	}

	public int 		getMoney() 	{ return money; }
	public String 	getId() 	{ return id; }
	public String	getPwd() 	{ return pwd; }
	public void setId(String id) {
		this.id = id;
	}
	public void setPwd(String pwd) {
		this.pwd = pwd;
	}
	public void setMoney(int money) {
		this.money = money;
	}
	
	public void deposit(int money2) {
		this.money += money2;
		System.out.println("입금 후 잔액은 "+ this.money + "원 입니다.");
	}
	public void withdraw(int money2) {
		if (this.money - money2 < 0) {
			System.out.println("잔액이 부족합니다.");
		} else { 
		this.money -= money2;
		System.out.println("출금 후 잔액은 "+ this.money + "원 입니다.");
		}
	}




}
```

<br/>

## BankManager

<br/>

```java
package BankProject;
import java.util.*;

public class BankManager {
	private static BankManager instance = new BankManager(); // 싱글톤. static 필수!
	private ArrayList<Account> accounts;
	Scanner sc = new Scanner(System.in);
	private BankManager() {
		accounts = new ArrayList<Account>();
	}
	
	public static BankManager getInstance() { // static 필수!
		return instance;
	}
	public int showMenu() {
		int choice = 0;
		System.out.printf("====================\n"
				 + "1. Join\n"
				 + "2. Login\n"
				 + "3. Exit\n"
				 + "====================\n"
				 + "번호를 입력하세요 : ");
		choice = sc.nextInt();
		return choice;
	}
	public void join() {
		System.out.println("생성할 아이디를 입력하세요.");
		String id = sc.next();
		System.out.println("생성할 패스워드를 입력하세요.");
		String pwd = sc.next();
		System.out.println("초기 입금액을 입력하세요.");
		int initMoney = sc.nextInt();
		accounts.add(new Account(id, pwd, initMoney));
	}
	public Account login() { //로그인
		System.out.print("로그인 할 아이디를 입력하세요.");
		String id = sc.next();
		System.out.print("패스워드를 입력하세요.");
		String pwd = sc.next();
		for (Account a : accounts)
			if(a.getId(). equals(id) && a.getPwd().equals(pwd))
				return a; // 고객이 입력한 정보와 어카운트 안의 정보가 맞으면 고객의 주소 반환.
		return null; // 고객이 없는 경우.
		

	}

	public int showBankMenu() {
		int sel = 0;
		System.out.printf(
				   "====================\n"
				 + "1. Deposit\n"
				 + "2. Withdraw\n"
				 + "3. Check the Balance\n"
				 + "4. Logout\n"
				 + "====================\n"
				 + "번호를 입력하세요 : \n");	
		
		sel = sc.nextInt();
		return sel;
	}

	public void deposit(Account acc, int money) {
		System.out.printf("입금할 금액 입력 : ");
		int deposit = sc.nextInt();
		acc.deposit(deposit);
		System.out.println("이전 메뉴로 돌아갑니다. \n" 
						 + ".\n"
						 + ".\n"
						 + ".\n");		
	}
	public void withdraw(Account acc) {
		System.out.println("출금할 금액 입력 : ");
		int withdraw = sc.nextInt();
		acc.withdraw(withdraw);
		System.out.println("이전 메뉴로 돌아갑니다. \n" 
						 + ".\n"
						 + ".\n"
						 + ".\n");

	}
	public void check(Account acc) {
		System.out.println("잔액은 "+ acc.getMoney() + "원 입니다.");
		System.out.println("이전 메뉴로 돌아갑니다. \n" 
						 + ".\n"
						 + ".\n"
						 + ".\n");		
	}
	
}
```
<br/>

## BankTest

<br/>

```java
package BankProject;
import java.util.*;
public class BankTest {
	
	public static void main(String[] args) {
		BankManager manager = BankManager.getInstance();

		do {
			int choice = manager.showMenu();
			switch( choice ) {
			case 1 : // Join
				manager.join();break;
			case 2 : // Login
				Account acc = manager.login();
				if(acc != null) {
					System.out.println("로그인 성공.");
					System.out.println(acc);
					System.out.println(acc.getId());
					System.out.println(acc.getPwd());
					System.out.println(acc.getMoney());
					do {
						int sel = manager.showBankMenu();
						switch(sel) {
							case 1: //입금
								int money = 0;
								manager.deposit(acc, money);
								break;
							case 2: //출금
								manager.withdraw(acc);
								break;
							case 3: //조회
								manager.check(acc);
								break;
							case 4: // logout
								

								break;
							default : System.out.println("다시 입력하세요 : ");
						}
					} while(true);
				} else 
					System.out.println("로그인 실패.");
				break;
			case 3 : // Exit
				System.out.println("종료합니다.");
				System.exit(0);
				break;
			default : System.out.println("다시 입력하세요 : ");
			}
		} while(true);
	}	

}
 ```
