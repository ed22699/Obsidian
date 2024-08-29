A good way to deal with a `int[][]` where you do not know the length it will be
- create with `List<int[]> output = new ArrayList<>()`
- turn to array with `output.toArray(new int[output.size()][]);`