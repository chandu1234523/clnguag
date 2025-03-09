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
