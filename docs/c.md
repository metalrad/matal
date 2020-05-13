#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<math.h>
#define N 4 
#define EPSILON 1.0E-5
#define TRUE 1
#define FALSE 0

	

int main()
{
	int sweep();
	int i,j;
	//int sw=0;

	double a[N][N]={0};//左辺
	double x[N],b[N]={0};//右辺
	int sw;
	
	a[0][0]=2; a[0][1]=3; a[0][2]=1; a[0][3]=4;
    a[1][0]=4; a[1][1]=1; a[1][2]=-3 ; a[1][3]=-2;
    a[2][0]=-1; a[2][1]=2; a[2][2]=2; a[2][3]=2;

	printf("=== 係数行列と定数 ===");
	for(i=0;i<N;i++);
	{
		for(j=0;j<N;i++){ printf("%10.4f",a[i][j]);	}
		printf("10.4f\n\n",b[i]);
	
	}
	sw=TRUE;

	sweep(&sw);

	if(sw==TRUE)
	{
		printf("\n\n === 掃出法による連立一次方程式の解 ===\n\n");
		for(i=0;i<N;i++) printf("x[%d] = %10.4f\n",i+1,x[i]);
	
	}
	else
	{
		printf("解は求められませんでした\n\n");
	}


	return 0;

}

void swap(double *wk1,double *wk2)
{
	//double wk1,wk2;
	double w;
	w=*wk1; *wk1=*wk2; *wk2=w;
}
int sweep(double a[N][N], double b[N], double x[N])
	{
		int i,j,k,ik;
		double ak,aik,ww;
		int sw;
		
		for(k=0;k<N;k++)
		{
			ak=a[k][k];

		if(fabs(ak)<=EPSILON)
		{
		ik=k+1;
		while((ik<N)&&(fabs(a[ik][k])<EPSILON)) ik++;
		if(ik<N)
		{
			for(j=k;j<N;j++) {swap(&a[k][j],&a[ik][j]);}
			swap(&b[k],&b[ik]);
			ak=a[k][k];
		}
		else
		{
			printf("ピボットが0です\n");
			sw=FALSE;
			goto owari;
		}
	}
	for(j=k;j<N;j++) a[k][j]=a[k][j]/ak;
	b[k]=b[k]/ak;
	for(i=0;i<N;i++)
	{
	if(i!=k)
	{
		aik=a[i][k];
		for(j=k;j<N;j++) a[i][j]=a[i][j]-aik*a[k][j];
		b[i]=b[i]-b[k]*aik;
	}
}
		
}

for(k=0;k<N;k++) 
	x[k]=b[k];
owari:;

}


【実行すると】
・数値がおかしい
・無限に実行される

【エラー】
1>------ ビルド開始: プロジェクト: itijihouteisiki, 構成: Debug Win32 ------
1>C:\Windows\Microsoft.NET\Framework\v4.0.30319\Microsoft.Common.Targets(983,5): warning MSB3644: フレームワーク ".NETFramework,Version=v4.0" の参照アセンブリが見つかりませんでした。これを解決するには、このフレームワーク バージョンの SDK または Targeting Pack をインストールするか、SDK または Targeting Pack をインストールしているフレームワークのバージョンにアプリケーションを再ターゲットしてください。アセンブリはグローバル アセンブリ キャッシュ (GAC) から解決され、参照アセンブリの代わりに使用されるため、アセンブリが目的のフレームワークに正しくターゲットされない場合もあります。
1>  kadai2.c
1>c:\users\owner\desktop\遠隔授業(と課題)\課題\数値解析\itijihouteisiki\itijihouteisiki\kadai2.c(61): warning C4101: 'ww' : ローカル変数は 1 度も使われていません。
1>c:\users\owner\desktop\遠隔授業(と課題)\課題\数値解析\itijihouteisiki\itijihouteisiki\kadai2.c(103): warning C4716: 'sweep' : 値を返さなければいけません
1>  itijihouteisiki.vcxproj -> C:\Users\owner\Desktop\遠隔授業(と課題)\課題\数値解析\itijihouteisiki\Debug\itijihouteisiki.exe
========== ビルド: 1 正常終了、0 失敗、0 更新不要、0 スキップ ==========
