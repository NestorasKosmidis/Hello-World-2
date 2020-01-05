var List, k, i, Max_value, Min_value;

function listsRepeat(value, n) {
  var array = [];
  for (var i = 0; i < n; i++) {
    array[i] = value;
  }
  return array;
}

function mathRandomInt(a, b) {
  if (a > b) {
    // Swap a and b to ensure a is smaller.
    var c = a;
    a = b;
    b = c;
  }
  return Math.floor(Math.random() * (b - a + 1) + a);
}

function textToTitleCase(str) {
  return str.replace(/\S+/g,
      function(txt) {return txt[0].toUpperCase() + txt.substring(1).toLowerCase();});
}

function listsGetSortCompare(type, direction) {
  var compareFuncs = {
    "NUMERIC": function(a, b) {
        return parseFloat(a) - parseFloat(b); },
    "TEXT": function(a, b) {
        return a.toString() > b.toString() ? 1 : -1; },
    "IGNORE_CASE": function(a, b) {
        return a.toString().toLowerCase() > b.toString().toLowerCase() ? 1 : -1; },
  };
  var compare = compareFuncs[type];
  return function(a, b) { return compare(a, b) * direction; }
}


List = listsRepeat(1, 15);
command.writeLine(List);
if (!List.length) {
  command.write('Need filled list to continue');
} else {
  for (k = 1; k <= 15; k++) {
    List[(i - 1)] = mathRandomInt(0, 20);
    i = (typeof i == 'number' ? i : 0) + 1;
  }
  command.writeLine('');
  command.writeLine(List);
  Max_value = Math.max.apply(null, List);
  command.writeLine('');
  command.writeLine('max value is :');
  command.writeLine(Max_value);
  command.writeLine((Max_value % 2 == 0 ? textToTitleCase('Άρτιος') : textToTitleCase('Περιττός')));
  command.writeLine('');
  Min_value = Math.min.apply(null, List);
  if (Min_value == 1) {
    command.writeLine(('min value is :'.toLowerCase()));
    command.writeLine(Min_value);
  } else if (Min_value == 0) {
    command.writeLine(('min value is :'.toLowerCase()));
    command.writeLine(Min_value);
  } else {
    command.writeLine((textToTitleCase('min value is higher than usual:')));
    command.writeLine(Min_value);
  }
  command.writeLine('');
  List = List.slice().sort(listsGetSortCompare("NUMERIC", 1));
  command.write(List);
}
