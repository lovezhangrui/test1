#includ<stdio.h>

void main(){

InitStack(S);

    InitQueue(Q);

printf("                                                              \n");

printf("                                                              \n");

printf("                    欢迎进入停车场系统\n");

printf("            **********************************************\n");

printf("                   1  新车到来    \n");

printf("                   2  车离开      \n");

printf("                   3  查看车场信息  \n");

printf("                   4  查看便道信息  \n");

printf("                   #  退出        \n");

printf("                计科高职13-3：齐工合伙人        \n");

printf("            **********************************************\n");

char cc;

cc=' ';

while(cc!='#'){

printf("请选择操作: ");

 cc=getchar();

        getchar();

switch (cc){

 case'1': Car_Come(S,Q);break;

     case'2': Car_leave(S,Q);break;

 case'3': seeStack(S);break;

 case'4': seeQueue(Q);break; 

 case'#': break;

        default:{printf("选择不正确！请重新选择！\n");

 

 continue;

 }

}

}

}

void seeStack(SqStack S){

if(StackEmpty(S)==-1){

printf("站内没有车！ \n");

return;

}

else{

while(StackEmpty(S)!=-1){

      Pop(S,tempCar);

  printf("%d 位置：%-10s  进站时间：%d\n",S.top,tempCar.carLicense,tempCar.time);

}

}

printf("------------------------------------------- \n");

}

void seeQueue(LinkQueue Q){

   if(QueueEmpty(Q)==-1){

printf("便道内没有车！ \n");

return;

}

else{

       InitQueue(tempQ);

printf("便道内车辆： \n");

while(QueueEmpty(Q)!=-1){

       DeQueue(Q,tempCar);

   printf(" %s \n",tempCar.carLicense);

EnQueue(tempQ,tempCar.carLicense);

}

//重新进队列

while(QueueEmpty(tempQ)!=-1){

       DeQueue(tempQ,tempCar);

   EnQueue(Q,tempCar.carLicense);

}

}

   printf("------------------------------------------- \n");

void Car_Come(SqStack &S,LinkQueue &Q){

printf("新车到来：\n");

printf("输入车牌号：");

scanf("%s",&tempCar.carLicense);

if(StackFull(S)==-1){

EnQueue(Q,tempCar.carLicense);

printf("此车辆已进入便道！\n");

}

else{

  printf("输入车进入停车场时间：");

  scanf("%d",&tempCar.time);

  getchar();

  Push(S,tempCar.carLicense,tempCar.time);

  printf("在停车场中的位置: %d\n",(S.top-1));

}

printf("----------------------------");

}

void Car_leave(SqStack &S,LinkQueue &Q)

{

    int d,come_time=0;

char car_license[15];

    printf("车辆离开车站：");

printf("请输入要离开车辆的位置：");

scanf("%d",&d);

if(StackEmpty(S)==-1){

return;

}

else{

if(d<S.top){

InitStack(tempS);

 while(S.top!=(d+1)){

     Pop(S,tempCar);

 Push(tempS,tempCar.carLicense,tempCar.time);

   }

       Pop(S,tempCar);

   come_time=tempCar.time;

   printf("输入车离开时间：");

   scanf("%d",&tempCar.time);

   printf("%s 已经离开!\n",tempCar.carLicense);

   printf("离开时间:%d\n",tempCar.time);

       printf("费用：%d \n",unit_price*(tempCar.time-come_time)); 

   //重新进栈

        while(StackEmpty(tempS)!=-1){

     Pop(tempS,tempCar);

 Push(S, tempCar.carLicense,tempCar.time);         

   }

if(QueueEmpty(Q)==-1){

return;

    }

else{

      DeQueue(Q,tempCar);

  printf("%s 进站\n",tempCar.carLicense);

      printf("输入车进站时间：");

      scanf("%d",&tempCar.time);

  Push(S,tempCar.carLicense,tempCar.time);

  printf("在停车场中的位置: %d\n",(S.top-1));

}

}

printf("----------------------------");

}

void InitStack(SqStack &S){

S.elem=(CarType *)malloc((N+1)*sizeof(CarType));

if(S.elem==NULL)

return;

S.top=0;

}

int StackEmpty(SqStack S){

if(S.top==0)

return -1;

}

int StackFull(SqStack S){

 

if(S.top==N)

return -1;

}

void GetTop(SqStack S,CarType &e){

if(S.top==0)

return;

e=S.elem[S.top-1];

}

void Push(SqStack &S,char *ch,int time){ 

if(S.top<N+1){

strcpy(S.elem[S.top].carLicense,ch);

S.elem[S.top].time=time; 

    S.top++;

}

}

void Pop(SqStack &S,CarType &eCar){

if(S.top==0)

return;

--S.top;

strcpy(eCar.carLicense,S.elem[S.top].carLicense);

eCar.time=S.elem[S.top].time;

}

void InitQueue(LinkQueue &Q){

Q.front=Q.rear=(QueuePtr)malloc(sizeof(QNode));

if(Q.front==NULL)

return;

Q.front->next=NULL;

}li

int QueueEmpty(LinkQueue Q){

if(Q.front==Q.rear)

return -1;

}

void EnQueue(LinkQueue &Q,char *ch){

p=(QueuePtr)malloc(sizeof(QNode));

if(p==NULL)

return;

strcpy(p->data.carLicense,ch);

p->next=NULL;

Q.rear->next=p;

Q.rear=p;

}

void DeQueue(LinkQueue &Q,CarType &eCar){

if(Q.front==Q.rear)

return;

p=Q.front->next;

strcpy(eCar.carLicense,p->data.carLicense);

Q.front->next=p->next;

if(Q.rear==p)

Q.rear=Q.front; 

free(p);

}
