import java.util.*;

public class Main {
    static int n;
    static int[][] a;

    // Function to calculate indegree of each vertex
    static int[] calculateIndegree(int[][] a) {
        int[] indegree = new int[n];
        for (int j = 0; j < n; j++) {
            indegree[j] = 0;
            for (int i = 0; i < n; i++) {
                if (a[i][j] != 0)
                    indegree[j]++;
            }
        }
        return indegree;
    }

    // Function to perform source removal method
    static void source_removal(int[] indegree) {
        boolean[] removed = new boolean[n];
        boolean cycle = false;

        for (int r = 0; r < n; r++) {
            int j;
            for (j = 0; j < n; j++) {
                if (indegree[j] == 0 && !removed[j]) {
                    break;
                }
            }

            // If no source vertex found (j == n), then graph is cyclic
            if (j == n) {
                cycle = true;
                break;
            }

            // Remove source vertex
            removed[j] = true;

            // Remove all outgoing edges from vertex j
            for (int k = 0; k < n; k++) {
                if (a[j][k] != 0) {
                    indegree[k]--;
                    a[j][k] = 0;
                }
            }
        }

        if (cycle) {
            System.out.println("Graph is cyclic, so no solution.");
        } else {
            System.out.println("BUILD SUCCESSFUL");
        }
    }

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.print("Enter the number of vertices: ");
        n = s.nextInt();
        a = new int[n][n];

        System.out.println("Enter the adjacency matrix:");
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                a[i][j] = s.nextInt();

        int[] indegree = calculateIndegree(a);
        source_removal(indegree);

        s.close();
}
}

//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

import java.io.PrintStream;
import java.util.Random;
import java.util.Scanner;

public class Main {
    static int count;

    public Main() {
    }

    static int partition(int[] a, int l, int r) {
        int i = l;
        int pivot = a[i];
        int j = r + 1;

        int temp;
        do {
            do {
                i++;
                ++count;
            } while(i < r && a[i] <= pivot);

            do {
                j--;
                ++count;
            } while(j > l && a[j] >= pivot);

            if (i < j) {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        } while(i < j);

        temp = a[l];
        a[l] = a[j];
        a[j] = temp;
        return j;
    }

    static void sort(int[] a, int l, int r) {
        if (l < r) {
            int s = partition(a, l, r);
            sort(a, l, s - 1);
            sort(a, s + 1, r);
        }

    }

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.print("Enter the number of elements: ");
        int n = s.nextInt();
        int[] a = new int[n];
        Random r = new Random();
        System.out.println("Generated Array: ");

        for(int i = 0; i < n; ++i) {
            a[i] = r.nextInt(100);
        }

        System.out.println("\nSorting...");
        sort(a, 0, n - 1);
        System.out.println("\nTotal number of basic operations performed: " + count);
        PrintStream var10000 = System.out;
        double var10001 = (double)n;
        double var10002 = Math.log((double)n);
        var10000.println("Lower Bound: " + var10001 * (var10002 / Math.log(2.0)));
        System.out.println("Upper Bound: " + n * n);
        s.close();
    }
}
