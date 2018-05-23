
``` C
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <windows.h> 
#define ADUSER_NAME "admin"
#define ADPASSWORD "Admin"
typedef struct Student //类型首字母大写以和变量区分 
{
	char cName[20];
	char iNumber[10];
	int  Score;
	struct Student  *next; 
} STU;//因为类型相同所以递归定义
int icount;//全局定义链表长度
int judgeadmin = -1;
void SetPos(int x,int y);
void Show();
int Login();
int Menu_select() ;
void Head();
STU* Creat();
void Print(STU *phead);
STU *Insert(STU *pHead);
void sort(STU* pHead);
void Delete(STU*pHead,int index);
STU* delHead(STU *pHead);
STU* FreeAll_LINK(STU*pHead);
void Search_stu(STU* pHead);
void Revise_stu(STU *pHead);
void Caozuowei();
void Chachong(STU *pHead); 
void Save_inf(STU*pHead);
STU* Dataread_inf(); 
int main()
{

	Show();
	Login();


	int iN;
	while(judgeadmin)
	{
		iN = Menu_select();
		//创建链表和录入链表都围绕头结点，在主函数使用一样
		STU *phead ;
		switch(iN)
		{
			case 0:
				getch();
				fflush(stdin);
				exit(0); 
			case 1: 
//								               创建 
				phead = Creat(); 
				
			//	FreeAll_LINK(phead);
				break;
			case 2:						 		
										//	打印
				Print(phead);
				break;	
			case 3:								//追加 
				
				phead = Insert(phead);
				
				break;
			case 4:
				
				for(int in = 1; in <= 3 ; in++)
				{ 
					Sleep(200);
					printf("."); 
				} 					
				system("CLS");
				Head();	puts("");								//排序 
				printf("\t\t\t\t*************数据排序************\n") ;
				sort(phead);
				getch();
				Caozuowei();
				fflush(stdin);
				break;
			case 5:	
				Revise_stu(phead);
				break;
			case 6:	
			for(int in = 1; in <= 3 ; in++)
				{ 
					Sleep(200);
					printf("."); 
				} 					
				system("CLS");
				Head();	puts("");							//删除 
				printf("\t\t\t\t*************删除学生信息************\n\t\t\t\t请选择删除方式。\n\t\t\t\t1)删除输入的序号对应的学生。\t2)删除全部学生\n\t\t\t\t"); 
				char ccho;
				ccho = getche();
				if(ccho != '1' && ccho != '2')
					break;
				else if(ccho == '1')
				{
					int index;//要删除的学生序号
					printf("\n\t\t\t\t请输入要删除的学生序号：\n\t\t\t\t");
					scanf("%d",&index);
					getchar();
					if(index != 1)
						Delete(phead,index);
					else
					{
						phead =  delHead(phead);
					}	
				}
				else
				{
					phead = FreeAll_LINK(phead);
					for(int in = 1; in <= 3 ; in++)
					{ 
						Sleep(200);
						printf("."); 
					} 
					printf("\n\t\t\t\t已清空！");	
				}	
				getch();
				Caozuowei();
				fflush(stdin);
				break;
			case 7:
				Search_stu(phead);
				break;			
		
		}
		system("CLS");
		
	}
	
} 



void SetPos(int x,int y)				//光标调整 
{
	COORD pos;
	HANDLE handle;
	pos.X=x;
	pos.Y=y;
	handle=GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleCursorPosition(handle,pos);
	
}	
void Show()
{
	int i;
	int x = 10,y = 6,x1 = 100,y1 = 7;
	int x2 = 10,y2 = 8,x3 = 100,y3 =9 ;
	int x4 = 10,y4 = 10,x5 = 100,y5 = 11;
	int x6 = 10,y6 = 12,x7 = 100,y7 = 13;
	int x8 = 10,y8 = 14,x9 = 100,y9 = 15;
	int x10 = 10,y10 = 16;
	for(i = 0; i < 31; i++,x+=3,x1-=3,x2+=3,x3-=3,x4+=3,x5-=3,x6+=3,x7-=3,x8+=3,x9-=3,x10+=3)
	{
		SetPos(x,y);
		printf("* *");
		Sleep(1);
		SetPos(x1,y1);
		printf("* *");
		Sleep(0.5);
		SetPos(x2,y2);
		printf("* *");
		Sleep(1);
		SetPos(x3,y3);
		printf("* *");
		Sleep(0.5);
		SetPos(x4,y4);
		printf("* *");
		Sleep(1);
		SetPos(x5,y5);
		printf("* *");
		Sleep(0.5);
		SetPos(x6,y6);
		printf("* *");
		Sleep(1);
		SetPos(x7,y7);
		printf("* *");
		Sleep(0.5);
		SetPos(x8,y8);
		printf("* *");
		Sleep(1);
		SetPos(x9,y9);
		printf("* *");
		Sleep(0.5);
		SetPos(x10,y10);
		printf("* *");
		Sleep(1);
	}
	x = 21;y = 9;
	for(i = 0; i < 345; i++,x++)
	{
		SetPos(x,y);
		printf(" ");
		Sleep(1);
		if(x ==89)
		{
			printf("\n");
			y++;
			x = 20;
		}
	}
	x = 45; y = 11;
	SetPos(x,y);
	printf("欢迎使用本操作系统！"); 
	x = 90,y = 20;
	SetPos(x,y);
	printf("作者：鲍小海");
	SetPos(x,y+1);
	printf("版本号：5.0");
	x = 20;y = 22;
	for(i = 0; i < 35; i++,x+=2)
	{
		SetPos(x,y);
		printf("—-");
		Sleep(10);
		if(x == 140)
		{
			printf("\n");
			y++;
			x = 0;
		}
	}SetPos(20,23);
	printf("要进入登录界面请按任意键\t\t\t要退出程序请按Esc键\n");
	char kjcz;
	kjcz = getche(); 
	if(kjcz == 0x1b)
	exit(0);
	system("cls"); 
} 

int Login()
{
	Head();
	printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n");
		printf("\n\n\n");
		printf("\t\t\t\t        ——       LOGIN     ——        \n");
		printf("\n\n\n");
		printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * \n");
	printf("\n\n\n\t\t\t\t\t您是否想以管理员身份登录？\n\n\t\t\t\t\t1 . 是\t\t0 . 否"); 
	char num;
	num = getch();
	while(num != '1' && num != '0')
	{ 
		printf("\n");
		printf("非法录入，请重新输入\n");
			num = getch();																				
		} 		
	if(num = '1')
	{
		system("cls");
		Head();
		printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n");
		printf("\n\n\n");
		printf("\t\t\t\t        ——       LOGIN     ——        \n");
		printf("\n\n\n");
		printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * \n");
		char username[50];
		char password[50];
		printf("\n\n\n\t\t\t请输入用户名及密码\n\n");
		printf("\t\t\t\t\t用户名：");
		int x, y;
		SetPos(50,16);
		printf("┏┈┈┈┈┈┈┈┈┈┈┈┈┈┓");  
		SetPos(50,17);
		printf("☆　　　　 　 ☆");
		SetPos(50,18);
		printf("┗┈┈┈┈┈┈┈┈┈┈┈┈┈┛"); 
		SetPos(52,17);
		scanf("%s",username);
		printf("\n\n");
		SetPos(30,21);
		printf("\t\t密码： ") ;
		SetPos(50,20);
		printf("┏┈┈┈┈┈┈┈┈┈┈┈┈┈┓");  
		SetPos(50,21);
		printf("☆　　　　　　☆");
		SetPos(50,22);
		printf("┗┈┈┈┈┈┈┈┈┈┈┈┈┈┛"); 
		SetPos(52,21);

		int i = 0,n = 5;
		char ch; 
		while((ch = getch())!='\r')
		{
			fflush(stdin);
			 if(ch == '\b')
        	 { 
            	if(i>0)
            	{
                	i--;
                	printf("\b \b");
                	password[i] = 0;
                	continue;
            	}
            	else
            	{
                	printf("\a");     //没有内容的时候
                	continue;
             	}
             }
       		 else
        	 {
            	password[i] = ch;
            	printf("*");
        	 }
 
        i++;
		}
		if(strcmp(username,ADUSER_NAME)==0 && strcmp(password,ADPASSWORD) == 0)
		{
			printf("\n\t\t登录成功！");
			printf("\n\t\t欢迎您，管理员！"); 
			printf("\n\n将在3 秒后跳转...");
			Sleep(3000);
			system("CLS");
		}
		else
		{
			SetPos(70,21);
			printf("用户名或密码错误，您还有一次机会\n");
		//	system("pause");
			x = 17;y = 25;
			for(i = 0; i < 35; i++,x+=2)
			{
				SetPos(x,y);
				printf("—-");
				Sleep(10);
			}
			SetPos(20,26);
			printf("要重新登录请按任意键\t\t要退出程序请按Esc键\n");
			char cho;
			cho = getch();
			if(cho == 0x1b)
			exit(0);
			system("cls");
			
			Head();
			printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n");
			printf("\n\n\n");
			printf("\t\t\t\t    ——       LOGIN     ——        \n");
			printf("\n\n\n");
			printf("\t\t  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * \n"); 
	 
			char username[50];
			char password[50];
			printf("\n\n\n\t\t请输入用户名及密码\n\n");
			printf("\t\t\t\t\t用户名：");
			SetPos(50,16);
			printf("┏┈┈┈┈┈┈┈┈┈┈┈┈┈┓");  
			SetPos(50,17);
			printf("☆　　　　 　 ☆");
			SetPos(50,18);
			printf("┗┈┈┈┈┈┈┈┈┈┈┈┈┈┛"); 
			SetPos(52,17);
			scanf("%s",username);
			printf("\n\n");
			SetPos(30,21);
			printf("\t\t密码： ") ;
			SetPos(50,20);
			printf("┏┈┈┈┈┈┈┈┈┈┈┈┈┈┓");  
			SetPos(50,21);
			printf("☆　　　　 　 ☆");
			SetPos(50,22);
			printf("┗┈┈┈┈┈┈┈┈┈┈┈┈┈┛"); 
			SetPos(52,21);
			 i = 0,n = 5;
			char ch; 
			while((ch = getch())!='\r')
			{
				fflush(stdin);
				 if(ch == '\b')
	        	 { 
	            	if(i>0)
	            	{
	                	i--;
	                	printf("\b \b");
	                	password[i] = 0;
	                	continue;
	            	}
	            	else
	            	{
	                	printf("\a");     //没有内容的时候
	                	continue;
	             	}
	             }
	       		 else
	        	 {
	            	password[i] = ch;
	            	printf("*");
	        	 }
	 
	        i++;
			}
			if(strcmp(username,ADUSER_NAME)==0 && strcmp(password,ADPASSWORD) == 0)
			{
				printf("\n\t\t登录成功！");
				printf("\n\t\t欢迎您，管理员！"); 
				printf("\n\n将在3 秒后跳转...");
				Sleep(3000);
				system("CLS");
			}
				else
				{
					for(i = 3; i != 0; i--)
					{ 
						printf("\n\n登录异常，本系统将在%d秒后自动关闭...\n",i);
						Sleep(1000);
					} 
					exit(0); 
				}
		}
	}
	
	
//	else
//	{
//		//学生端登录，只实现查询功能；
//		 
//	}
}

	

int Menu_select()                              //菜单选择系统函数  
{  
     char c;   
	printf("\t\t\t\t\t╭═════════■□■□═══╮\n");  
	printf("\t\t\t\t\t    学生信息管理系统\t  管理端 \n");  
	printf("\t\t\t\t\t╰═══■□■□══════════╯\n");  
	printf("\t\t\t\t *  *  *  *  *  *  *  *  *  *  *  *  *  *\n") ;
	printf("\t\t\t\t  ↗—————————————————↖\n\n\n");  
	printf("\t\t\t\t  │ 1. 创建表单\t           2. 显示记录 │\n\n\n");  
	printf("\t\t\t\t  │                                    │\n\n");  
	printf("\t\t\t\t  │ 3. 增加信息\t           4. 数据排序 │\n\n\n");  
	printf("\t\t\t\t  │                 ★                 │\n\n");  
	printf("\t\t\t\t  │ 5. 修改记录\t           6. 删除记录 │\n\n\n");  
	printf("\t\t\t\t  │                                    │\n\n");  
	printf("\t\t\t\t  │ 7. 信息查询\t           0. 退出程序 │\n\n\n");  
	printf("\t\t\t\t  ↘—————————————————↙\n\n");
	SetPos(0,0);
	int m,n,k,l;
	m = 25,n = 10,k = 82,l = 10;
	for(int i = 0; i < 10; i++,n++,l++)
	{
		
		printf("*\n");
		Sleep(15);
		SetPos(k,l);
		 printf("*\n");
		Sleep(15);
		SetPos(m,n);
	
	}printf("*");
	int x,y;int a,b;
	x = 7;y = 7;a = 100;b = 7;
	SetPos(x,y);
	for(int i = 0; i < 20; i++,y++,b++)
	{
		
		printf("*\n");
		Sleep(10);
		SetPos(a,b);
		 printf("*\n");
		Sleep(10);
		SetPos(x,y);
	
	}
	x = 7;y = 28;a = 100;b = 28;
	for(int i = 0; i < 30; i++,x++,a--)
	{
		printf("*");
		Sleep(10);
		SetPos(a,b);
		printf("*");
		SetPos(x,y);
	}printf("\t\t请输入操作项：");   
        c=getche(); 
		
	while(c < '0' || c > '7')
	{
		system("cls");
		printf("\t\t\t\t\t╭═════════■□■□═══╮\n");  
		printf("\t\t\t\t\t    学生信息管理系统\t  管理端 \n");  
		printf("\t\t\t\t\t╰═══■□■□══════════╯\n");  
		printf("\t\t\t\t *  *  *  *  *  *  *  *  *  *  *  *  *  *\n") ;
		printf("\t\t\t\t  ↗—————————————————↖\n\n\n");  
		printf("\t\t\t\t  │ 1. 创建表单\t           2. 显示记录 │\n\n\n");  
		printf("\t\t\t\t  │                                    │\n\n");  
		printf("\t\t\t\t  │ 3. 增加信息\t           4. 数据排序 │\n\n\n");  
		printf("\t\t\t\t  │                 ★                 │\n\n");  
		printf("\t\t\t\t  │ 5. 修改记录\t           6. 删除记录 │\n\n\n");  
		printf("\t\t\t\t  │                                    │\n\n");  
		printf("\t\t\t\t  │ 7. 信息查询\t           0. 退出程序 │\n\n\n");  
		printf("\t\t\t\t  ↘—————————————————↙\n\n"); 
		SetPos(0,0);
		m = 25,n = 10,k = 82,l = 10;
		for(int i = 0; i < 10; i++,n++,l++)
		{
			
			printf("*\n");
			SetPos(k,l);
			 printf("*\n");
			SetPos(m,n);
		
		}printf("*");
		
		x = 7;y = 7;a = 100;b = 7;
		SetPos(x,y);
		for(int i = 0; i < 20; i++,y++,b++)
		{
			
			printf("*\n");
			SetPos(a,b);
			 printf("*\n");
			SetPos(x,y);
		
		}
		x = 7;y = 28;a = 100;b = 28;
		for(int i = 0; i < 30; i++,x++,a--)
		{
			printf("*");
			SetPos(a,b);
			printf("*");
			SetPos(x,y);
		}printf("\t\t请输入操作项："); 
			c = getche();
			system("CLS");
		}
		return c-'0';
	
}  
void Head()
{
	printf("\t\t\t\t\t╭═════════■□■□═══╮\n");  
	printf("\t\t\t\t\t    学生信息管理系统\t  管理端 \n");  
	printf("\t\t\t\t\t╰═══■□■□══════════╯\n");  
}
STU* Creat()//创建并输入链表函数 
{
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 					
	system("CLS");
	Head();	
	printf("\t\t\t\t本操作项将建立新的名单，您是否想要继续？\n\t\t\t\t继续请按1\t退出请按任意键。\n\n\t\t\t\t");
	char cho;
	cho = getche();
	if(cho == '1')
	{  
		for(int in = 1; in <= 3 ; in++)
		{ 
			Sleep(200);
			printf("."); 
		} 	
		system("CLS");
		Head();	puts("");
		printf("\t\t\t\t*************创建名单************\n"); 
		STU*pHead = NULL;
		STU *pNew ,*pEnd; //定义新节点，原结点（新节点前面那个，此处定义只是命名） 
		icount = 0;
		pNew = pEnd = (STU *)malloc(sizeof(STU));//此时所谓新结点和原结点都在同一空间
		//录入
		printf("\t\t\t\t请输入学生的信息：\n");
		printf("\t\t\t\t学号为0时停止录入(此次录入信息不包含在内)\n");
	
		printf("\t\t\t\t学号：\n\t\t\t\t");
		scanf("%s",pNew->iNumber);
		printf("\t\t\t\t姓名：\n\t\t\t\t"); 
		scanf("%s",pNew->cName);
		printf("\t\t\t\t成绩：\n\t\t\t\t");
		scanf("%d",&pNew->Score);
		if(pNew->Score < 0|| pNew->Score > 100)
		{
			printf("\t\t\t\t请合法输入学生信息");
			return 0; 
		}
		printf("\n\n");
		/*说明，关于以上取址符的问题
		        指针应该指向地址（空间）所以应该加上取址符；
				%s不加的原因是所指向字符数组名name本身就是地址；*/
		char null[10] = {"0"};
		while(1)//设置录入终止条件	
		{
			//循环内处理录入的变量
			icount++;
			if(icount == 1)//分为第一个结点和其他结点两种情况 
			{
				pNew->next = pHead;
				
				pEnd = pNew;//此时新即头即尾 
				 pHead = pNew;
			} 
			else
			{
				pNew->next = NULL;
				pEnd->next = pNew;
				pEnd = pNew;
				/*原来的尾结点指向新结点，新结点位于链表末尾作尾结点*/
				/*现在再次分配内存空间为了下次录入*/
			}
			pNew = (STU*)malloc(sizeof(STU));
			printf("\t\t\t\t学号：\n\t\t\t\t");
			scanf("%s",pNew->iNumber);
			if(strcmp(pNew->iNumber,null) == 0)
			{
				break;
			}
			printf("\t\t\t\t姓名：\n\t\t\t\t");  
			scanf("%s",pNew->cName);
			printf("\t\t\t\t成绩：\n\t\t\t\t");
			scanf("%d",&pNew->Score);
			if(pNew->Score < 0||pNew->Score > 100)
			{
			printf("\t\t\t\t请合法输入学生信息");
			return 0; 
			}
			printf("\n\n");		
				//如此循环直到不符合录入条件 
			
		}
		printf("\t\t\t\t");
			for(int in = 1; in <= 3 ; in++)
			{ 
				Sleep(200);
				printf("."); 
			} 
			printf("\n\t\t\t\t创建并录入成功！");
		free(pNew);
	//	Save_inf(pHead);
		getch();
		Caozuowei();
		fflush(stdin);
		return pHead;
	} 
}
void Print(STU *phead)						//输出函数
{ 
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 					
	system("CLS");
//	phead = Dataread_inf()	;
	Head();	puts("");
	STU *ptemp;
	int index = 1;
	printf("\t\t\t\t*************本名单共有%d名学生************\n",icount);
	ptemp = phead; 
	if(icount == 0)
	{
		printf("\n\n\t\t\t\t名单为空");
		return ;
	} 
	while(ptemp != NULL)
	{
		printf("\t\t\t\t第%d名学生是：\n",index);
		printf("\t\t\t\t");
		puts(ptemp->cName);
		printf("\t\t\t\t学号：%s\n\t\t\t\t姓名： %s\n\t\t\t\t成绩： %d\n\n",ptemp->iNumber,ptemp->cName,ptemp->Score);	
		ptemp = ptemp->next;
		index++;
	} 
	Chachong(phead);
	getch();
	Caozuowei();
	fflush(stdin);
}
STU *Insert(STU *pHead)//添加单个学生信息（尾插） 
{
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 					
	system("CLS");
	Head();	printf("\n");
	printf("\t\t\t\t*************增加学生信息************\n") ;
	STU*p = pHead,*pNew;
	pNew = (STU*)malloc(sizeof(STU));
	printf("\t\t\t\t学号：\n\t\t\t\t");
	scanf("%s",pNew->iNumber);
	printf("\t\t\t\t姓名：\n\t\t\t\t"); 
	scanf("%s",pNew->cName);
	printf("\t\t\t\t成绩：\n\t\t\t\t");
	scanf("%d",&pNew->Score);
	printf("\n\n");		
	while(p->next != NULL)
	p = p->next;
	p->next = pNew;
	pNew->next = NULL;
	icount++;
	printf("\t\t\t\t");
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 
	printf("\n\t\t\t\t添加成功！"); 
	getch();
	Caozuowei();
	return pHead;
}

void sort(STU* pHead)
{
	int temp ;char ci[10];char cn[20];
	STU * p = pHead,*q,*s;
	printf("\t\t\t\t请选择您想用哪种方式排序。\n\t\t\t\t1)按成绩由高到低排序 \t2)按学号由小到大排序\n\t\t\t\t");
	char ccho;
	fflush(stdin);
	ccho = getche();
	if(ccho != '2' && ccho != '1')
	{ 
		printf("\t\t\t\t无效输入"); 
		return; 
	}
	else if(ccho == '1')
	{
		if(p == NULL)
		{
			printf("\n\t\t\t\t该名单为空\n");
		}
		else
		{
			while(p->next != NULL)
			{
				q=p;//q初始化
				s=p->next;
				while(s!=NULL)
				{
					if(q->Score <  s->Score)
						q=s;//q记录最小节点位置
					s=s->next;//遍历
				}
				if(q!=p)//若q值改变，交换
				{
					temp=q->Score; strcpy(ci , q->iNumber); strcpy(cn , q->cName);
					q->Score=p->Score; strcpy(q->iNumber,p->iNumber); strcpy(q->cName,p->cName); 
					p->Score=temp;strcpy(p->iNumber,ci); strcpy(p->cName,cn);
				}
				p=p->next;//下一轮回交换位置
			}
			printf("\n\t\t\t\t");
			for(int in = 1; in <= 3 ; in++)
			{ 
				Sleep(200);
				printf("."); 
			} 
			printf("\n\t\t\t\t排序成功！");
		}
	}
	else if(ccho == '2')
	{
		if(p == NULL)
		{
			printf("\n该名单为空\n");
		}
		else
		{
			while(p->next != NULL)
			{
				q=p;//q初始化
				s=p->next;
				while(s!=NULL)
				{
					if(strcmp(q->iNumber, s->iNumber) == 1)
						q=s;//q记录最小节点位置
					s=s->next;//遍历
				}
				if(q!=p)//若q值改变，交换
				{
					temp=q->Score; strcpy(ci , q->iNumber); strcpy(cn , q->cName);
					q->Score=p->Score; strcpy(q->iNumber,p->iNumber); strcpy(q->cName,p->cName); 
					p->Score=temp;strcpy(p->iNumber,ci); strcpy(p->cName,cn);
				}
				p=p->next;//下一轮回交换位置
			}
			printf("\n\t\t\t\t");
			for(int in = 1; in <= 3 ; in++)
			{ 
				Sleep(200);
				printf("."); 
			} 
			printf("\n\t\t\t\t排序成功！");
		}
	}
} 
void Delete(STU*pHead,int index)
{
//	printf("请选择删除方式。\n1)删除输入的序号对应的学生。\t2)删除全部学生\n"); 
	int i;
	
	printf("\t\t\t\t正在删除第%d名学生\t\t\t\t",index);
	if(index > icount)
	{
		for(int in = 1; in <= 3 ; in++)
		{ 
		Sleep(200);
		printf("."); 
		} 
		printf("\n\t\t\t\t没有找到对应学生的信息，删除失败！");
		return; 
	}
	STU*pTemp;
	pTemp = pHead;
	STU*pPre;
	pPre = pTemp;
	for(i = 1; i < index; i++)
	{
		pPre = pTemp;
		pTemp = pTemp->next;
		
	}
	pPre->next = pTemp->next;
	free(pTemp);
	icount--;
	printf("\n\t\t\t\t"); 
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 
	printf("\n\t\t\t\t删除成功！"); 
}
STU* delHead(STU *pHead)
{ 	
	STU*p = pHead;
	pHead=p->next;
    free(p); 
    icount--;
    printf("\n\t\t\t\t");
    for(int in = 1; in <= 3 ; in++)
			{ 
				Sleep(200);
				printf("."); 
			} 
			printf("\n\t\t\t\t删除成功！"); 
    return 	pHead;
}
STU* FreeAll_LINK(STU*pHead)
{
	STU * p = pHead;
	while(pHead != NULL)
	{
		//记录结点 
		p = pHead;
		//向后移动 
		pHead = p->next;
		 
		free(p);
		icount = 0;
	}
	return(pHead);
	 
}
void Search_stu(STU* pHead)
{
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 					
	system("CLS");
	Head();	puts("");
	char ccho;
	printf("\t\t\t\t请选择您想要的查询方式\n\t\t\t\t1)按学号查询 \t2)按姓名查询\n\t\t\t\t"); 
	ccho = getche(); 
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 	
	while(ccho != '1' && ccho != '2')
	{
		printf("\t\t\t\t无效输入！");
		printf("\n");
		ccho = getche(); 
	} 
	 if(ccho == '1')
	{ 
		char siNumber[10];
		int p = 0;
		printf("\n\t\t\t\t请输入要查询的学生学号\n\t\t\t\t");
		scanf("%s",siNumber);
		STU* pTemp = pHead;
		while(pTemp != NULL)
		{
			if(strcmp(pTemp->iNumber,siNumber) == 0)
			{
				p++;
				printf("\t\t\t\t该学生信息如下：\n\t\t\t\t姓名： %s\n\t\t\t\t学号： %s\n\t\t\t\t成绩：%d\n",pTemp->cName,pTemp->iNumber,pTemp->Score);
				break;
			}
			pTemp = pTemp->next;
		}
		if(p == 0)
		printf("\t\t\t\t没有找到对应的学生信息。"); 
	}
	else
	{
		char scName[20];
		int p = 0;
		printf("\n\t\t\t\t请输入要查询的学生姓名\n\t\t\t\t");
		scanf("%s",scName);
		STU* pTemp = pHead;
		while(pTemp != NULL)
		{
			if(strcmp(pTemp->cName,scName) == 0)
			{
				p++;
				printf("\t\t\t\t该学生信息如下：\n\t\t\t\t姓名： %s\n\t\t\t\t学号： %s\n\t\t\t\t成绩：%d\n\t\t\t\t",pTemp->cName,pTemp->iNumber,pTemp->Score);
				break;
			}
			pTemp = pTemp->next;
		}
		if(p == 0)
		printf("\t\t\t\t没有找到对应的学生信息。");
	} 
	getch();
	Caozuowei();
	fflush(stdin);	
	
} 
void Revise_stu(STU *pHead)
{
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 			
			
	system("CLS");
	Head();	puts("");
	char ccho;
	printf("\t\t\t\t请选择您想要的修改方式：\n\t\t\t\t1) 修改指定学号的学生\t2) 修改指定姓名的学生\n\t\t\t\t");
	ccho = getche(); 
	for(int in = 1; in <= 3 ; in++)
	{ 
		Sleep(200);
		printf("."); 
	} 	
	while(ccho != '1' && ccho != '2')
	{
		printf("\t\t\t\t无效输入！");
		printf("\n\t\t\t\t");
		ccho = getche(); 
	} 
	 if(ccho == '1')
	{ 
		char siNumber[10];
		int p = 0;
		printf("请输入要修改的学生学号\n\t\t\t\t");
		scanf("%s",siNumber);
		STU* pTemp = pHead;
		while(pTemp != NULL)
		{
			if(strcmp(pTemp->iNumber,siNumber) == 0)
			{
				p++;
				printf("\t\t\t\t该学学号：生原信息如下：\n\t\t\t\t姓名： %s\n\t\t\t\t学号： %s\n\t\t\t\t成绩：%d\n\n\t\t\t\t将修改为\n\t\t\t\t",pTemp->cName,pTemp->iNumber,pTemp->Score);
				printf("\n");
				printf("\t\t\t\t姓名：\n\t\t\t\t"); 
				scanf("%s",pTemp->cName);
				printf("\t\t\t\t学号：\n\t\t\t\t") ;
				scanf("%s",pTemp->iNumber);
				printf("\t\t\t\t成绩：\n\t\t\t\t");
				scanf("%d",&pTemp->Score);
				printf("\n");
				for(int in = 1; in <= 3 ; in++)
				{ 
					Sleep(200);
					printf("."); 
				} 
				printf("\n\t\t\t\t修改成功！"); 
				break;
			}
			pTemp = pTemp->next;
		} 
		if(p == 0)
		printf("\t\t\t\t没有找到对应的学生信息。"); 
	}
	else
	{
		char scName[20];
		int p = 0;
		printf("\n\t\t\t\t请输入要修改的学生姓名\n\t\t\t\t");
		scanf("%s",scName);
		STU* pTemp = pHead;
		while(pTemp != NULL)
		{
			if(strcmp(pTemp->cName,scName) == 0)
			{
				p++;
				printf("\t\t\t\t该学生原信息如下：\n\t\t\t\t姓名： %s\n\t\t\t\t学号： %s\n\t\t\t\t成绩：%d\n\n\t\t\t\t将修改为：",pTemp->cName,pTemp->iNumber,pTemp->Score);
				printf("\n");
				printf("\t\t\t\t姓名：\n\t\t\t\t"); 
				scanf("%s",pTemp->cName);
				printf("\t\t\t\t学号：\n\t\t\t\t"); 
				scanf("%s",pTemp->iNumber);
				printf("\t\t\t\t成绩：\n\t\t\t\t");
				scanf("%d",&pTemp->Score);
				printf("\n");
				for(int in = 1; in <= 3 ; in++)
				{ 
					Sleep(200);
					printf("."); 
				} 
				printf("\n\t\t\t\t修改成功！"); 
				break;
			}
			pTemp = pTemp->next;
		}
		if(p == 0)
		printf("\t\t\t\t没有找到对应的学生信息。");
		getch();
		Caozuowei();
		fflush(stdin);
	} 
} 
void Caozuowei()
{
	int i;
//	int i,x,y;
//	x = 17;y = 28;
	printf("\n\n\n\t ");
	for(i = 0; i < 30; i++)
	{
		printf("—-");
		Sleep(10);
	}
//	SetPos(20,29);
	printf("\n\t\t\t   ");
	printf("要返回主菜单请按任意键\t\t要退出程序请按Esc键\n");
	char cho;
	cho = getch();
	if(cho == 0x1b)
	exit(0);
}
void Chachong (STU*pHead)
{
	int i,j,index = 0;
	STU* p,*s;
	s = pHead;
	p = pHead->next;
	for(i = 1; i < icount; i++)
	{
		for(j = 0; j < i-1; j++)
		{
			if(strcmp(s->iNumber,p->iNumber) == 0)
			{
				index++;
				printf("发现重复学生信息：");
				printf("\n\t\t\t\t姓名： %s\n\t\t\t\t学号： %s\n\t\t\t\t成绩：%d\n\n",s->cName,s->iNumber,s->Score);
		    } 
			s = s->next;
		}
		p = p->next;
	}
	
}
//文件操作
//将链表信息保存到文件中 
void Save_inf(STU*pHead)
{
	STU* ptemp;
	FILE* fp;
	if((fp = fopen("e:\\wj\\test.txt","wt")) == NULL)
	{
		printf("诶呀，出错啦");
		 return;
	}	
	for(ptemp = pHead; ptemp != NULL; ptemp = ptemp->next)
	{
		fprintf(fp,"%s %s %d\n",ptemp->iNumber,ptemp->cName,ptemp->Score);
	}
		printf("\n保存成功，任意键退出");
		getch();
		fclose(fp);
		
}
//读取文件中的内容到单链表
STU* Dataread_inf()
{
	STU*pHead,*r,*p;
	FILE*fp;
	if((fp = fopen("e:\\wj\\test.txt","rt")) == NULL)
	{
		printf("诶呀!出错了QAQ");
		return 0 ;
		 
	}
	pHead = (STU*)malloc(sizeof(STU));
	pHead->next = NULL;
	r = pHead;
	while(!feof(fp))
	{
		p = (STU*)malloc(sizeof(STU));
		fscanf(fp,"%s %s %d",p->iNumber,p->cName,&p->Score);
		r = p;
		
	}
	r->next = NULL;
	fclose(fp);
	printf("读取成功");
	getch();
	return(pHead); 
} 

```
