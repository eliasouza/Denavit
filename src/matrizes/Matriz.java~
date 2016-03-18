package matrizes;
import java.util.ArrayList;
import java.util.List;
/**
 * @author Eias Gonçalves
 * esgoncalves@ime.eb.br
 * 13/07/2015
 */
public class Matriz {
    private static final int T = 4;  
    private static int i, l, c, k;
    
    /*Inicializa as matrizes; Essa função recebe os parâmetros de D&H e 
    inicializa as matrizes*/
    public static ArrayList<double[][]> gerarMatriz(double[] q, 
            double[] a, double d[], double[] alpha, int n){
        List M = new ArrayList<double[][]>();                  
        for(i=0; i<n; i++){                        
            double[][] A = new double[][]{
                {Math.cos(q[i]), ((-Math.sin(q[i]))*Math.cos(alpha[i])),
                 (Math.sin(q[i])*Math.sin(alpha[i])), 
                 (a[i]*Math.cos(q[i]))},
                
                {Math.sin(q[i]), (Math.cos(q[i])*Math.cos(alpha[i])), 
                 ((-Math.cos(q[i]))*Math.sin(alpha[i])), 
                 (a[i]*Math.sin(q[i]))},
                
                {0, Math.sin(alpha[i]), Math.cos(alpha[i]), d[i]},
                
                {0, 0, 0, 1}};
            M.add(A);
        }               
        return (ArrayList<double[][]>) M;
    }
    
    /*Calcular matrizes; Essa função recebe as matrizes e realiza o 
      cálculo.*/
    public static void calcularMatrizes6DOF(double[][] A, double[][] B, 
              double[][] C, double[][] D, double[][] E, double[][] F, int n){
        double[] q = new double[n];
        double soma;
        double[][] temp1 = new double[T][T], temp2 = new double[T][T], 
                   temp3 = new double[T][T];
        
        //temp1 = A*B
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += A[l][k] * B[k][c];}
                temp1[l][c] = soma;
            }
        }
        //temp2 = temp1*C
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp1[l][k] * C[k][c];}
                temp2[l][c] = soma;
            }
        }
        
        //temp1 = temp2*D
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp2[l][k] * D[k][c];}
                temp1[l][c] = soma;
            }
        }
        
         //temp3 = temp1*E
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp1[l][k] * E[k][c];}
                temp3[l][c] = soma;
            }
        }
        
        //temp1 = temp3*F
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp3[l][k] * F[k][c];}
                temp1[l][c] = soma;
            }
        }
        
        /*
        //temp1 = D*E
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += D[l][k] * E[k][c];}
                temp1[l][c] = soma;
            }
        }
        
        //temp3 = temp1*F
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp1[l][k] * F[k][c];}
                temp3[l][c] = soma;
            }
        }
        
        //temp1 = temp2*temp3
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp2[l][k] * temp3[k][c];}
                temp1[l][c] = soma;
            }
        }
        */
                    
        //Recuperar vetor de "q" da matriz total:
        for(l=0; l<3; l++){
            q[l] = temp1[l][3];
        }
        
        //Imprimir o vetor "q":
         System.out.print("["); 
         for(l=0; l<3; l++){
             System.out.print(q[l]);
             if(l!=2){System.out.print("  ");}
         }System.out.println("]");
    }
    
    public static ArrayList<double[]> calcularMatrizes3DOF(
            double[][] A, double[][] B, double[][] C, int n
    ){
        double[] q = new double[n];
        double soma;
        double[][] temp1 = new double[T][T], temp2 = new double[T][T];
        
        //Parâmetros do Jacobiano:
        double[] p0 = {0, 0, 0};
        double[] p1 = new double[n];
        double[] p2 = new double[n];
        double[] p3 = new double[n];
        double[] z0 = {0, 0, 1};//idem para z1 e z2
        ArrayList<double[]> pontos = new ArrayList<>();
        
        //temp1 = A*B
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += A[l][k] * B[k][c];}
                temp1[l][c] = soma;
            }
        }        
        
        //temp2 = temp1*C
        for(l=0; l<T; l++){
            for(c=0; c<T; c++){
                soma = 0;
                for(k=0;k<T;k++){soma += temp1[l][k] * C[k][c];}
                temp2[l][c] = soma;
            }
        }                     
        
        //Recuperar P1, P2 e P3:
        for(l=0; l<3; l++){
            p1[l] = A[l][3];    //A
            p2[l] = temp1[l][3];//A*B
            p3[l] = temp2[l][3];//A*B*C
        }
        
        pontos.add(p0);
        pontos.add(p1);
        pontos.add(p2);
        pontos.add(p3);
        pontos.add(z0);
  
        //Imprimir o vetor "q":
         System.out.println("ROBÔ PLANAR");
         System.out.print("Vetor q = ["); 
         for(l=0; l<3; l++){
             System.out.print(p3[l]);
             if(l!=2){System.out.print("  ");}
         }System.out.println("]\n");
        
         return pontos;
    }
    
    private static double[] produtoVetorial(double[] z, double[] sub, int n){
        double[] mult = new double[n];
        mult[0] = (z[1]*sub[2] - sub[1]*z[2]);
        mult[1] = (z[2]*sub[0] - sub[2]*z[0]);
        mult[2] = (z[0]*sub[1] - sub[0]*z[1]);        
        return mult;
    }
    
    public static void calcularJacobiano(ArrayList<double[]> pontos, int n){
        //Variáveis do jacobiano recuperadas:
        double[] p0 = pontos.get(0);
        double[] p1 = pontos.get(1);
        double[] p2 = pontos.get(2);
        double[] p3 = pontos.get(3);
        double[] z  = pontos.get(4);// z0, z1 e z2 são iguais;
        double[] sub = new double[n];
        double[] mult = new double[n];        
        
        //Limpar array de pontos para reutilizar:
        pontos.clear();
                
        //z0 x (p3-p0) linha a linha:
        for(i=0; i<n; i++){
            sub[i] = p3[i] - p0[i];                
        }               
        pontos.add(produtoVetorial(z, sub, n));//Jv1
        
        //z1 x (p3-p1) linha a linha:
        for(i=0; i<n; i++){
            sub[i] = p3[i] - p1[i];
        }
        pontos.add(produtoVetorial(z, sub, n));//Jv2
        
        //z2 x (p3-p2) linha a linha:
        for(i=0; i<n; i++){
            sub[i] = p3[i] - p2[i];    
        }
        pontos.add(produtoVetorial(z, sub, n));//Jv3
                        
       //Reutilizar vetor de posições p/ velocidade linear: 
       p0 = pontos.get(0);//Jv1
       p1 = pontos.get(1);//Jv2
       p2 = pontos.get(2);//Jv3
       
       //Preencher a matriz jacobiana:
       double[][] J = new double[][]{
        {p0[0], p1[0], p2[0]},
        {p0[1], p1[1], p2[1]},
        {p0[2], p1[2], p2[2]},
        {z[0],  z[0],  z[0]},
        {z[1],  z[1],  z[1]},
        {z[2],  z[2],  z[2]}
       };
       
        System.out.println("Jacobiano algébrico:");
       for(i=0; i<(2*n); i++){
           for(c=0; c<n; c++){
               System.out.print(J[i][c] + "\t");
           }
           System.out.print("\n");
       }
    }
}
