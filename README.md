# Minimum-Moves-to-Zero

In a kingdom, a wizard has a magic number . To break the spell and turn into 0, he can perform one of two actions: add or subtract any power of 2. What’s the minimum number of moves the wizard needs to make the magic number equal to 0?

import java.util.*;

public class Main {
    static class Pair<K, V> {
        private K key;
        private V value;

        public Pair(K key, V value) {
            this.key = key;
            this.value = value;
        }

        public K getKey() {
            return key;
        }

        public V getValue() {
            return value;
        }
    }
    public static int minimumMovesToZero(int n) {
        Queue<Pair<Integer, Integer>> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();

        queue.offer(new Pair<>(n, 0));
        visited.add(n);

        while (!queue.isEmpty()) {
            Pair<Integer, Integer> front = queue.poll();
            int current = front.getKey();
            int steps = front.getValue();
            for (int i = 0; ; ++i) {
                int powerOf2 = (1 << i); 
                if (powerOf2 > Math.abs(current)) break;
                int nextAdd = current + powerOf2;
                if (!visited.contains(nextAdd)) {
                    if (nextAdd == 0) return steps + 1;
                    queue.offer(new Pair<>(nextAdd, steps + 1));
                    visited.add(nextAdd);
                }
                int nextSubtract = current - powerOf2;
                if (!visited.contains(nextSubtract)) {
                    if (nextSubtract == 0) return steps + 1;
                    queue.offer(new Pair<>(nextSubtract, steps + 1));
                    visited.add(nextSubtract);
                }
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(minimumMovesToZero(n));
    }
}
