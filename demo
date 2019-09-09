#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<conio.h>
#include<io.h>

#define COLS 80

typedef struct Dex {
	int orderid;//序号
	char indexid[11];//学号
}Dex;

typedef struct Stu {
	int sign;//是否需要删除的标志
	char name[21];
	int sex;//1为男生，0为女生
	char id[11];
	double grade;
}Stu;


char *Menu[] = {
	"--------学生管理系统--------\n",
	"1.信息录入         (A)\n",
	"2.信息修改         (B)\n",
	"3.信息查询         (C)\n",
	"4.添加信息         (D)\n",
	"5.删除信息         (E)\n",
	"6.学生信息打印     (F)\n",
	"0.退出             (G)\n",
};

void showMessageCenter(char *str);
void showMainMenu();
int fwriteFile(FILE *fp);
int writeFile();
void exchangeFile();
int searchFile();
void addFile(int m);
void deleteFile();
void readFile();


void readFile() {
	FILE *fp;
	int i = 0,k = 0;
	Stu student[50];

	fp = fopen("studentMessage.txt","rb");
	if(NULL == fp) {
		printf("打开文件失败!");
		return ;
	}
	while(fread(&student[k],sizeof(Stu),1,fp)) {
		k++;
	}
	for(i=0;i<k;i++) {
		printf("\n姓名  性别  学号    成绩\n");
		printf("%4s%5d%6s%13f",student[i].name,student[i].sex,student[i].id,student[i].grade);
	}
	printf("\n");

	fclose(fp);
	showMainMenu();
}


void deleteFile() {
	FILE *fp;
	Stu student[50];
	char id[11];
	int i=0,k=0;

	fp = fopen("studentMessage.txt","rb");
	if(NULL == fp) {
		printf("打开文件失败!");
		return ;
	}
	while(fread(&student[k],sizeof(Stu),1,fp)) {
		k++;
	}
	printf("\n请输入要删除的学生学号：");
	flushall();
	gets(id);
	//逻辑删除
	for(i=0;i<k;i++) {
		if(!strcmp(student[i].id,id))
			student[i].sign = 0;
			
	}
	
	fclose(fp);
	remove("studentMessage.txt");

	//物理删除
	fp = fopen("studentMessage.txt","w+");
	if(NULL == fp) {
		printf("打开文件失败!");
		return ;
	}
	for(i=0;i<k;i++) {
		if(0 != student[i].sign)
			fwrite(&student[i],sizeof(Stu),1,fp);

	}
	printf("\n\n删除完成!\n");

	fclose(fp);
	//system("cls");
	showMainMenu();

}

void addFile(int m) {
	FILE *fp;
	int n;
	int s;

	fp = fopen("studentMessage.txt","a");
	if(NULL == fp) {
		printf("打开文件失败!");
		return;
	}
	printf("\n请输入要加入的学生信息：\n\n");
	n = fwriteFile(fp);
	s = n+m;
	printf("\n\n添加学生信息成功!\n");

	fclose(fp);
	//system("cls");
	showMainMenu();
}

int searchFile() {
	FILE *fp;
	Stu student[50];
	int i=0,k=0;
	char id[11];

	fp = fopen("studentMessage.txt","rb");
	if(NULL == fp) {
		printf("打开文件失败!");
		return 0;
	}
	while(fread(&student[k],sizeof(Stu),1,fp)) {
		k++;
	}
	printf("\n请输入要查找的学生学号:");
	flushall();
	gets(id);
	for(i=0;i<k;i++) {
		if(!strcmp(student[i].id,id))
			break;
	}
	printf("\n查找成功!\n");
	printf("\n\n所查找的学生信息：\n");
	printf("\n姓名  性别  学号    成绩\n");
	printf("%4s%5d%6s%13f\n",student[i].name,student[i].sex,student[i].id,student[i].grade);

	fclose(fp);
	return i;
	//system("cls");
	showMainMenu();
}

void exchangeFile() {
	FILE *fp;
	Stu student[50];
	char name[21];
	char exid[11];
	char id[11];
	int i=0,k=0;
	double g;

	fp = fopen("studentMessage.txt","r+");
	if(NULL == fp) {
		printf("打开文件失败!");
		return ;
	}
	printf("\n\n请输入要修改的学生学号：");
	flushall();
	gets(exid);
	while(fread(&student[k],sizeof(Stu),1,fp)) {
		k++;
	}
	fclose(fp);
	fp = fopen("studentMessage.txt","w+");
	for(i=0;i<k;i++) {
		if(!strcmp(student[i].id,exid)) {
			printf("\n请输入要修改的信息:\n");
			printf("\n姓名：");
			flushall();
			gets(name);
			strcpy(student[i].name,name);
			printf("\n性别（1位男生，0为女生）：");
			scanf("%d",&student[i].sex);
			printf("\n学号：");
			flushall();
			gets(id);
			strcpy(student[i].id,id);
			printf("\n成绩：");
			scanf("%lf",&g);
			student[i].grade = g;
			break;
		}
	}
	for(i=0;i<k;i++) {
		fwrite(&student[i],sizeof(Stu),1,fp);
	}
	printf("\n\n修改完成!\n");
	
	fclose(fp);
	//system("cls");
	showMainMenu();
}

int writeFile() {
	FILE *fp;
	int n;

	fp = fopen("studentMessage.txt","w+");
	if(NULL == fp) {
		printf("打开文件失败!");
		return 0;
	}
	n = fwriteFile(fp);
	printf("\n\n录入完成!\n");

	fclose(fp);
	//system("cls");
	showMainMenu();
	return n;
}

int fwriteFile(FILE *fp) {
	Stu student[50];
	int n;
	int i;
	char name[21];
	char id[11];
	double g;

	printf("输入信息的学生个数：");
	scanf("%d",&n);
	printf("\n请输入学生信息：\n");
	for(i=0;i<n;i++) {
		student[i].sign = 1;
	}
	for(i=0;i<n;i++) {
		printf("\n请输入第%d位同学信息：\n",i+1);
		printf("\n姓名：");
		flushall();
		gets(name);
		strcpy(student[i].name,name);
		printf("\n性别（1位男生，0为女生）：");
		scanf("%d",&student[i].sex);
		printf("\n学号：");
		flushall();
		gets(id);
		strcpy(student[i].id,id);
		printf("\n成绩：");
		scanf("%lf",&g);
		student[i].grade = g;
	}
	for(i=0;i<n;i++) {
		fwrite(&student[i],sizeof(Stu),1,fp);
	}
	system("cls");
	showMainMenu();

	return n;
}

void showMainMenu() {
	int i=0;
	int n;
	char ch;

	if(!access("studentMessage.txt",0)) {
		while(Menu[i]){
			showMessageCenter(Menu[i]);
			i++;
			if(8 == i) {
				break;
			}
		}
		printf("请输入选择：");
		flushall();
		scanf("%c",&ch);
		switch(ch) {
			case '1':n = writeFile();break;
			case 'A':n = writeFile();break;
			case '2':exchangeFile();break;
			case 'B':exchangeFile();break;
			case '3':i = searchFile();break;
			case 'C':i = searchFile();break;
			case '4':addFile(n);break;
			case 'D':addFile(n);break;
			case '5':deleteFile();break;
			case 'E':deleteFile();break;
			case '6':readFile();break;
			case 'F':readFile();break;
			case '0':break;
			case 'G':break;
			default:printf("\n没有该选项!请重新输入选择:\n\n");showMainMenu();
		}
	}
	i = 0;
	while(i<8){
		if(1 == i||7 == i) {
			showMessageCenter(Menu[i]);
			i++;
		}
		i++;
	}
	printf("请输入选择：");
	flushall();
	scanf("%c",&ch);
	switch(ch) {
		case '1':n = writeFile();break;
		case 'A':n = writeFile();break;
		case '0':break;
		case 'G':break;
		default:printf("\n学生信息未录入!请录入信息\n\n");showMainMenu();
	}
}

void showMessageCenter(char *str) {
	int i;
	int lenth;

	lenth = (COLS - strlen(str)) / 2;
	for(i = 0; i < lenth; i++) 
		printf(" ");
	printf("%s\n", str);
}

int main() {

	showMainMenu();

	return 0;
}
