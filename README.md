test
====
scrollPos = 0; scrollPos <= 24; scrollPos++
dg = 0; dg < 3; dg++
dp = scrollPos / 4 + dg
d = (x / (int)Math.pow(10, dp)) % 10
shift = (scrollPos % 4) - dg * 4
line |= charset[d * 5 + ln] >> shift
or
line |= charset[d * 5 + ln] << -shift

        int startX = -1, startY = -1, finishX = -1, finishY = -1;
        Queue<P> unvisited = new PriorityQueue<>();
        P map[][] = new P[dt.length][];
        for (int y = 0; y < dt.length; y++) {
            map[y] = new P[dt[0].length()];
            for (int x = 0; x < dt[0].length(); x++) {
                if (dt[y].charAt(x) == 'X') {
                    continue;
                }
                P p = new P();
                p.x = x;
                p.y = y;
                p.dist = Integer.MAX_VALUE - 1;
                if (dt[y].charAt(x) == 'S') {
                    startX = x;
                    startY = y;
                    p.dist = 0;
                }
                if (dt[y].charAt(x) == 'F') {
                    finishX = x;
                    finishY = y;
                }
                unvisited.add(p);
                map[y][x] = p;
            }
        }
        while (!unvisited.isEmpty()) {
            P current = unvisited.poll();
            current.visited = true;
            P next;
            if (current.x > 0 && (next = map[current.y][current.x - 1]) != null && !next.visited) {
                if (next.dist > current.dist + 1) {
                    unvisited.remove(next);
                    next.dist = current.dist + 1;
                    next.prev = current;
                    unvisited.add(next);
                }
            }
            if (current.x < dt[0].length() - 1 && (next = map[current.y][current.x + 1]) != null && !next.visited) {
                if (next.dist > current.dist + 1) {
                    unvisited.remove(next);
                    next.dist = current.dist + 1;
                    next.prev = current;
                    unvisited.add(next);
                }
            }
            if (current.y > 0 && (next = map[current.y - 1][current.x]) != null && !next.visited) {
                if (next.dist > current.dist + 1) {
                    unvisited.remove(next);
                    next.dist = current.dist + 1;
                    next.prev = current;
                    unvisited.add(next);
                }
            }
            if (current.y < dt.length - 1 && (next = map[current.y + 1][current.x]) != null && !next.visited) {
                if (next.dist > current.dist + 1) {
                    unvisited.remove(next);
                    next.dist = current.dist + 1;
                    next.prev = current;
                    unvisited.add(next);
                }
            }
        }
        Set<P> path = new HashSet<>();
        Stack<P> backtrace = new Stack<>();
        P current = map[finishY][finishX];
        while (current != null) {
            path.add(current);
            backtrace.push(current);
            current = current.prev;
        }
        current = backtrace.pop();
        while (!backtrace.isEmpty()) {
            //←↑→↓
            P next = backtrace.pop();
            if (next != null) {
                if (next.y < current.y) {
                    current.symbol = 'u';
                } else if (next.y > current.y) {
                    current.symbol = 'd';
                } else if (next.x > current.x) {
                    current.symbol = 'r';
                } else if (next.x < current.x) {
                    current.symbol = 'l';
                }
                current = next;
            }
        }
        for (int y = 0; y < dt.length; y++) {
            for (int x = 0; x < dt[0].length(); x++) {
                if (path.contains(map[y][x])) {
                    System.out.print('.');//map[y][x].symbol);
                } else {
                    System.out.print(dt[y].charAt(x));
                }
            }
            System.out.println();
        }
        System.out.println();
