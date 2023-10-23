import java.util.*;
import java.util.List;

class Graph {
    public HashMap<Integer, List<Integer>> graph;

    public Graph() {
        graph = new HashMap<>();
    }

    public void addEdge(int node, List<Integer> neighbors) {
        graph.put(node, neighbors);
    }
}

public class MatrixToGraphConverter {
    private static Graph matrixToGraph(int[][] matrix) {
        Graph graph = new Graph();
        int rows = matrix.length;
        int cols = matrix[0].length;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                int node = matrix[i][j];
                List<Integer> neighbors = new ArrayList<>();

                if (i > 0) {
                    neighbors.add(matrix[i - 1][j]);
                }
                if (i < rows - 1) {
                    neighbors.add(matrix[i + 1][j]);
                }
                if (j > 0) {
                    neighbors.add(matrix[i][j - 1]);
                }
                if (j < cols - 1) {
                    neighbors.add(matrix[i][j + 1]);
                }

                graph.addEdge(node, neighbors);
            }
        }

        return graph;
    }

    private static void bfs(Graph graph, int startNode) {
        HashSet<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new ArrayDeque<>();

        queue.offer(startNode);
        visited.add(startNode);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.println(node); // Replace with the desired action on the node

            for (int neighbor : graph.graph.get(node)) {
                if (!visited.contains(neighbor)) {
                    queue.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of rows: ");
        int rows = scanner.nextInt();
        System.out.print("Enter the number of columns: ");
        int cols = scanner.nextInt();

        int[][] matrix = new int[rows][cols];
        System.out.println("Enter the matrix elements:");

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        System.out.print("Enter the start element for BFS: ");
        int startNode = scanner.nextInt();

        scanner.close();

        Graph graph = matrixToGraph(matrix);
        bfs(graph, startNode);
    }
}
