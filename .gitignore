var nil = -1;
function Puzzle() {
    function h(a, b, c) {
        this.toString = function () {
            try {
                var a = "type: ";
                switch (this.type) {
                    case f.item.cell:
                        a += "C";
                        break;
                    case f.item.node:
                        a += "N";
                        break;
                    case f.item.hline:
                        a += "H";
                        break;
                    case f.item.vline:
                        a += "V";
                        break;
                    default:
                        a += this.type
                }
                a += ", x: " + this.x + ", y: " + this.y;
                a += ", v: " + this.value + ", s: " + this.solution;
                return a += ", w: " + this.count + ", w: " + this.work
            }
            catch (b) {
                throw f.exception(b), b;
            }
        };
        this.reset = function () {
            try {
                this.value = this.label = this.areas = this.solution = nil, this.error = this.count = this.color = this.state = this.clues = this.marks = 0, this.work = nil, this.fixed = !1, this.valid = !0, this.markers.clear()
            }
            catch (a) {
                throw f.exception(a), a;
            }
        };
        this.init = function () {
            try {
                for (var d = 0; d < this.length; d++)
                    for (var e in this)
                        "function" == typeof this[e] && (this[e].ojname = "i." + e);
                if (void 0 === a || null == a)a = nil;
                if (void 0 === b || null == b)b = nil;
                if (void 0 === c || null == c)c = f.item.cell;
                this.x = a;
                this.y = b;
                this.px = this.py = 0;
                this.type = c;
                this.markers = new q;
                this.reset()
            }
            catch (g) {
                throw f.exception(g), g;
            }
        };
        this.init()
    }

    function l() {
        var a = 0, b = 0, c = 0;
        this.start = function () {
            a = b = c = (new Date).getTime()
        };
        this.activity = function () {
            var a = (new Date).getTime();
            3E5 < a - c && (b = b - c + a);
            c = a
        };
        this.getElapsedTime = function () {
            this.activity("elapsed");
            return parseInt(((new Date).getTime() - a) / 1E3)
        };
        this.setElapsedTime = function (b) {
            a = (new Date).getTime() - 1E3 * b
        };
        this.getUsedTime = function () {
            this.activity("used");
            return parseInt(((new Date).getTime() - b) / 1E3)
        };
        this.setUsedTime = function (a) {
            b = (new Date).getTime() - 1E3 * a
        }
    }

    function p() {
        this.load = "load";
        this.save = "save";
        this.timing = "timing";
        this.solution = "solution";
        this.exception = "exception";
        this.exceptionSent = this.timingSent = !1;
        this.send = function (a, b) {
            try {
                var c = null;
                switch (a) {
                    case this.load:
                    case this.save:
                        c = f.config.loadsaveScript;
                        break;
                    case this.solution:
                        c = f.config.solutionScript;
                        break;
                    case this.timing:
                        if (this.timingSent)return;
                        c = f.config.timingScript;
                        this.timingSent = !0;
                        break;
                    case this.exception:
                        if (this.exceptionSent)return;
                        c = f.config.exceptionScript;
                        this.exceptionSent = !0
                }
                if (null == c)
                    return "";
                b || (b = " ");
                c += "?cmd=" + a + "&pid=" + f.level.pid + "&r=" + (f.level.rows ? f.level.rows : f.level.size) + "&c=" + (f.level.cols ? f.level.cols : f.level.size) + "&utime=" + f.timer.getUsedTime() + "&etime=" + f.timer.getElapsedTime() + "&score=" + f.score.current + "&ua=" + f.userAgentString + "&ref=" + f.config.documentName;
                f.paint();
                ojdebug("Server.url:", c);
                return this.read(c, b)
            }
            catch (d) {
                return ojdebug("server.send:", d.toString()), d.toString()
            }
        };
        this.read = function (a, b) {
            try {
                ojdebug("Server.read:", a);
                var c = new XMLHttpRequest;
                setTimeout(function () {
                    c && 4 != c.readyState && (ojdebug("ajax-request aborted by timeout"), c.abort())
                }, 5E3);
                b ? (c.open("POST", a, !1), c.setRequestHeader("Content-length", b.length.toString())) : (c.open("GET", a, !1), c.setRequestHeader("Content-length", "0"), navigator.userAgent.contains("MSIE") || c.overrideMimeType("text/plain; charset=ISO-8859-1"));
                c.setRequestHeader("Content-type", "text/plain");
                c.setRequestHeader("Connection", "close");
                c.setRequestHeader("Referer", f.config.documentName);
                c.send(b);
                if (!c.responseText)return "";
                try {
                    return decodeURIComponent(escape(c.responseText))
                }
                catch (d) {
                    return c.responseText
                }
            }
            catch (e) {
                return e.toString()
            }
        }
    }

    function q() {
        for (var a = [], b = 0; b < this.length; b++)
            for (var c in this)
                "function" == typeof this[c] && (this[c].ojname = "m." + c);
        this.clear = function (b, c) {
            if (0 != a.length) {
                if (b) {
                    c || (c = b);
                    for (var g = b; g <= c; g++)
                        a[g] = !1
                }
                else a = [];
                return !1
            }
        };
        this.length = function () {
            return a.length
        };
        this.cardinality = function () {
            if (0 == a.length)return 0;
            for (var b = 0, c = 0; c < a.length; c++)!0 == a[c] && b++;
            return b
        };
        this.toString = function () {
            for (var b = "", c = 0; c < a.length; c++)
                !0 == a[c] && (b += "ABCDEFGHIJ0123456789abcdefghijklmnopqrstuvwxyzKLMNOPQRSTUVWXYZ&$"[c]);
            return b
        };
        this.fromString = function (b) {
            this.clear();
            for (var c = 0; c < b.length; c++) {
                var g = "ABCDEFGHIJ0123456789abcdefghijklmnopqrstuvwxyzKLMNOPQRSTUVWXYZ&$".indexOf(b.charAt(c));
                -1 != g && (a[g] = !0)
            }
        };
        this.get = function (b) {
            return a[b]
        };
        this.set = function (b) {
            return a[b] = !0
        };
        this.toggle = function (b) {
            a[b] = a[b] ? !1 : !0;
            return a[b]
        }
    }

    function s() {
        this.isIndexed = this.isSession = this.isLocal = !1;
        this.isCookies = navigator.cookieEnabled;
        try {
            localStorage && (this.isLocal = !0), sessionStorage && (this.isSession = !0), indexedDB && (this.isIndexed = !0)
        }
        catch (a) {
        }
        this.setLocal = function (a, c, d) {
            try {
                return this.set(localStorage, a, c, d)
            }
            catch (e) {
                return !1
            }
        };
        this.setSession = function (a, c, d) {
            try {
                return this.set(sessionStorage, a, c, d)
            }
            catch (e) {
                return !1
            }
        };
        this.set = function (a, c, d, e) {
            try {
                if (!a)return !1;
                for (var g = new Date, f = g.valueOf(), k = a.length - 1; 0 <= k; k--) {
                    var m = a.getItem(a.key(k)), n = m.indexOf("|");
                    parseInt(m.substring(0, n)) < f && a.removeItem(a.key(k))
                }
                c = Math.abs(c.hash()).toString();
                e || (e = 10);
                g.setDate(g.getDate() + e);
                f = g.valueOf().toString();
                a.setItem(c, f + "|" + d);
                return !0
            }
            catch (h) {
                return !1
            }
        };
        this.getLocal = function (a) {
            try {
                return this.get(localStorage, a)
            }
            catch (c) {
                return null
            }
        };
        this.getSession = function (a) {
            try {
                return this.get(sessionStorage, a)
            }
            catch (c) {
                return null
            }
        };
        this.get = function (a, c) {
            try {
                if (!a)return null;
                c = Math.abs(c.hash()).toString();
                var d = a.getItem(c);
                if (d)var e = d.indexOf("|"), d = d.substring(e + 1);
                return d
            }
            catch (g) {
                return null
            }
        };
        this.setCookie = function (a, c, d) {
            try {
                if (!isCookies)return !1;
                var e = new Date;
                e.setDate(e.getDate() + d);
                document.cookie = escape(a) + "=" + escape(c) + "; expires=" + e.toUTCString();
                return !0
            }
            catch (g) {
                return this.exception(g), !1
            }
        };
        this.getCookie = function (a) {
            try {
                if (!this.isCookies)return null;
                for (var c = document.cookie.split(";"), d = 0; d < c.length; d++) {
                    var e = unescape(c[d]).trim().split("=");
                    if (a == e[0])return e[1]
                }
                return null
            } catch (g) {
                return this.exception(g), null
            }
        }
    }

    function v(a) {
        this.N = 624;
        this.M = 397;
        this.TEMPERING_MASK_B = 2636928640;
        this.TEMPERING_MASK_C = 4022730752;
        this.MATRIX_A = 2567483615;
        this.UPPER_MASK = 2147483648;
        this.LOWER_MASK = 2147483647;
        this.mt = [];
        this.mti = null;
        this.mag01 = [];
        this.init = function (a) {
            a || (a = (new Date).getTime());
            this.mt = Array(this.N);
            this.mt[0] = a & 4294967295;
            for (this.mti = 1; this.mti < this.N; this.mti++)
                this.mt[this.mti] = 69069 * this.mt[this.mti - 1] & 4294967295;
            this.mag01 = Array(2);
            this.mag01[0] = 0;
            this.mag01[1] = this.MATRIX_A
        };
        this.generate = function () {
            var a;
            if (this.mti >= this.N) {
                var c;
                for (c = 0; c < this.N - this.M; c++)
                    a = this.mt[c] & this.UPPER_MASK | this.mt[c + 1] & this.LOWER_MASK, this.mt[c] = this.mt[c + this.M] ^ a >>> 1 ^ this.mag01[a & 1];
                for (; c < this.N - 1; c++)
                    a = this.mt[c] & this.UPPER_MASK | this.mt[c + 1] & this.LOWER_MASK, this.mt[c] = this.mt[c + (this.M - this.N)] ^ a >>> 1 ^ this.mag01[a & 1];
                a = this.mt[this.N - 1] & this.UPPER_MASK | this.mt[0] & this.LOWER_MASK;
                this.mt[this.N - 1] = this.mt[this.M - 1] ^ a >>> 1 ^ this.mag01[a & 1];
                this.mti = 0
            }
            a = this.mt[this.mti++];
            a ^= a >>> 11;
            a ^= a << 7 & this.TEMPERING_MASK_B;
            a ^= a << 15 & this.TEMPERING_MASK_C;
            return a ^ a >>> 18
        }
        ;
        this.setSeed = function (a) {
            this.init(a)
        };
        this.getInt = function (a) {
            return Math.abs(this.generate()) % a
        };
        this.init(a)
    }

    var f = this;
    this.puzzleVersion = "7.2.34";
    this.copyrightString = "Copyright (c) 2003-2014 by Otto Janko";
    this.userAgentString = "Puzzle.Script." + this.puzzleVersion;
    this.config = {
        janko: !1,
        data: "",
        file: "",
        elem: "",
        appid: "oj-",
        mode: "task",
        modeTask: "task",
        modeGame: "game",
        modeMake: "make",
        modeEdit: "edit",
        unit: 0,
        level: 0,
        cookieName: "app_name",
        cookieMail: "app_mail",
        documentHost: document.location.host,
        documentHref: document.location.href,
        documentName: null,
        mailScript: null,
        timingScript: null,
        loadsaveScript: null,
        solutionScript: null,
        exceptionScript: null,
        touchscreen: !1,
        mobile: !1
    };
    (function () {
        var a = navigator.userAgent;
        if (a.contains("Android") || a.contains("iPhone") || a.contains("iPad") || a.contains("iPod") || a.contains("BlackBerry") || a.contains("Windows Phone") || a.contains("IEMobile") || a.contains("webOS") || a.contains("Opera Mini"))this.config.mobile = !0;
        this.config.touchscreen = "ontouchstart"in window || window.DocumentTouch && document instanceof DocumentTouch;
        this.config.documentHref.contains("ojtouch") && (this.config.touchscreen = !0);
        var a = this.config.documentHref, b = a.indexOf("#");
        -1 != b && (a = a.slice(0, b));
        b = a.indexOf("?");
        -1 != b && (a = a.slice(0, b));
        this.config.documentName = a
    }).apply(this);
    (function () {
        var a = this.config, b = a.documentHost, c = a.documentHref;
        this.config.janko = b.contains("janko.at") || b.contains("ojanko.at") || b.contains("127.0.0.1") || c.contains("/Usr-pr/") || c.contains("/Web/");
        this.config.janko && (b = "http://" + a.documentHost + "/", a.mailScript = b + "SendMail2.php", a.timingScript = b + "SendTiming.php", a.loadsaveScript = b + "Gamescore.php", a.solutionScript = b + "SendSolution2.php", a.exceptionScript = b + "SendException2.php")
    }).apply(this);
    this.enable = {
        check: !0,
        solve: !1,
        solution: !0,
        hint: !0,
        undoredo: !0,
        loadsave: !1,
        prevnext: !0,
        current: !0,
        colors: !0,
        smarkers: !0,
        vmarkers: !1,
        make: !1,
        reset: !1,
        rotate: !1,
        info: !0,
        edit: !1,
        options: !1,
        tools: !1,
        tilt: !1,
        zoom: !0,
        tier: !1,
        sendtime: !0,
        sendsol: !0,
        sendsave: !0,
        cells: !0,
        lines: !1,
        nodes: !1,
        pcells: !0,
        plines: !0,
        pnodes: !1,
        pgrid: !1,
        pgridlines: !0,
        pedgelines: !0,
        pcursor: !0,
        dragging: !1,
        keypad: !1,
        currentValue: !0
    };
    this.enable.loadsave = this.config.janko;
    this.overwritten = {makeMove2: !1, make2: !1, solve2: !1};
    this.flags = [];
    this.checking = {disable: 0, rules: "rules", solution: "solution", both: "both"};
    this.autoValueMarkers = this.editValueMarkers = !1;
    var t = null, w = null, u = "";
    this.keys = "author source rights solver title info pid unit size rows cols depth variant options layout infotext check mode seed score moves problem solution areas rlabels clabels nlabels cellmarkers celltext labels clues lines linemarkers linetext linelabels lineclues nodes nodemarkers nodetext nodelabels nodeclues".split(" ");
    this.levels = [];
    this.level = {nr: 0};
    this.board = {c: [], n: [], h: [], v: [], l: [], a: []};
    this.size = {x: nil, y: nil, z: nil};
    this.item = {cell: 0, node: 1, line: 2, hline: 6, vline: 10};
    this.labels = {north: 0, south: 0, east: 0, west: 0};
    this.cell = {values: null, min: 1, max: 0, nilalias: nil};
    this.line = {values: null, grid: nil, wall: 0, cross: 1, none: 3};
    this.node = {values: null};
    this.area = {black: nil - 1, outside: nil - 2, label: nil - 3, aside: nil - 4};
    this.marker = {
        symbolBase: 0,
        symbolLast: 9,
        numberBase: 10,
        numberLast: 19,
        letterBase: 20,
        letterLast: 45,
        circle: 0,
        square: 1,
        decagon: 2,
        cross: 3,
        dot: 4,
        letterA: 5,
        letterB: 6,
        letterC: 7,
        letterD: 8,
        letterX: 43
    };
    this.current = {item: null, marker: nil, color: 0, type: nil, value: nil, pvalue: nil};
    this.score = {current: 0, best: 0, high: 0, optimize: 0, minimize: 1, maximize: 2, label: null};
    this.moves = {
        list: null,
        last: -1,
        current: -1,
        disable: 0,
        collapse: !0,
        useMakeMoveForRedo: !0,
        typeVersion: "Z",
        typeCell: "M",
        typeNode: "N",
        typeVertical: "V",
        typeHorizontal: "H",
        typeAccept: "A",
        typeReject: "R",
        typeRemove: "Q",
        typeCheck: "C",
        typeSolve: "L",
        typeHint: "T",
        typeShowSolution: "S",
        typeInitValueMarkers: "I",
        typeUpdateValueMarkers: "U"
    };
    this.solved = !1;
    this.result = {code: 0, none: 0, won: 1, draw: 2, lost: 3};
    this.savedGames = [];
    this.timer = this.server = this.random = this.storage = null;
    this.run = function (a) {
        try {
            if (document.createElement("canvas").getContext) {
                this.storage = new s;
                this.random = new v;
                this.server = new p;
                this.timer = new l;
                for (var b = [this, this.timer, this.server, this.storage, this.keypad], c = ["p", "t", "v", "s", "k"], d = 0; d < b.length; d++)
                    for (var e in b[d])
                        "function" == typeof b[d][e] && (b[d][e].ojname = c[d] + "." + e);
                if (this.config.documentHref.contains("?")) {
                    for (var g = this.config.documentHref.split("?"), g = g[1].split("&"), d = 0; d < g.length; d++)g[d].startsWith("level=") && (this.config.level = parseInt(g[d].substring(6)));
                    for (d = 0; 10 > d; d++)this.flags[d] = g.contains("flag" + d)
                }
                this.overwritten.makeMove2 = !this.makeMove2.toString().contains("No item");
                this.overwritten.solve2 = !this.solve2.toString().contains("Solve2");
                this.overwritten.make2 = !this.solve2.toString().contains("Make2");
                "string" == typeof a ? this.config.data = a : (a.mode && (this.config.mode = a.mode), a.data && (this.config.data = a.data), a.file && (this.config.file = a.file), a.elem && (this.config.elem = a.elem), a.unit && (this.config.unit = a.unit), a.appid && (this.config.appid = a.appid), a.level && (this.config.appid = a.level));
                if (this.config.mode == this.config.modeGame)
                    this.config.unit && (this.level.unit = this.config.unit.toString());
                else {
                    if (this.config.data) {
                        var f = document.getElementById(this.config.data);
                        f && (w = t = f.innerHTML)
                    }
                    else
                        this.config.file ? w = t = this.server.read(this.config.file) : this.config.documentHref.contains("?") && (w = this.config.documentHref, this.readUrlParams());
                    if (!t) {
                        document.write("<p><b>" + this.uis.get("nodata") + "</b></p>");
                        return
                    }
                    (u = t.contains("<param") || t.contains("<PARAM") ? "param" : t.contains("<porom") || t.contains("<POROM") ? "porom" : "") && this.readAppletParams();
                    this.readData()
                }
                this.run2();
                this.config.level && (this.enable.prevnext = !1);
                this.onRun();
                0 == this.levels.length ? this.setup() : this.config.level ? this.select(this.config.level - 1) : this.select(0);
                setTimeout(this.run3.bind(this), 0)
            }
            else document.write("<p><b>" + this.uis.get("nocanvas") + "</b></p>")
        }
        catch (k) {
            this.exception(k)
        }
    };
    this.run2 = function () {
    };
    this.run3 = function () {
        try {
            if (this.paint(), this.config.janko && this.config.documentHref.startsWith("file")) {
                var a = "";
                0 == this.server.read("_ps.txt").length ? a = "cd" : 0 == this.server.read("_p.txt").length ? a = "c" : 0 == this.server.read("_s.txt").length && (a = "d");
                if (a)this.onSaveImage(a)
            }
        }
        catch (b) {
            this.exception(b)
        }
    };
    this.readUrlParams = function () {
        try {
            for (var a = document.location.href, a = a.substring(a.indexOf("?") + 1), b = a.split("&"), a = "", c = 0; c < b.length; c++) {
                var d = b[c].split("=");
                if (2 == d.length) {
                    var e = d[0], g = d[1];
                    "m" != e && "moves" != e && (g = g.replace(/\//g, ",").replace(/,,/g, ",-,").replace(/,,/g, ",-,"), "," == g.charAt(0) && (g = "-" + g), "," == g.charAt(g.length - 1) && (g += "-"), g = g.replace(/,/g, " "));
                    switch (e) {
                        case "z":
                            e = "size";
                            break;
                        case "r":
                            e = "rows";
                            break;
                        case "c":
                            e = "cols";
                            break;
                        case "d":
                            e = "depth";
                            break;
                        case "u":
                            e = "unit";
                            break;
                        case "p":
                            e = "problem";
                            break;
                        case "s":
                            e = "solution";
                            break;
                        case "m":
                            e = "moves";
                            break;
                        case "g":
                            e = "clues";
                            break;
                        case "a":
                            e = "areas";
                            break;
                        case "n":
                            e = "nodes";
                            break;
                        case "w":
                            e = "lines";
                            break;
                        case "rl":
                            e = "rlabels";
                            break;
                        case "cl":
                            e = "clabels"
                    }
                    a += e + " " + g + "\n"
                }
            }
            t = a
        }
        catch (f) {
            throw this.exception(f), f;
        }
    };
    this.readAppletParams = function () {
        try {
            for (var a = t, b = ""; a.contains("<param") || a.contains("<porom") || a.contains("<POROM");) {
                var c = a.indexOf("<param");
                -1 == c && (c = a.indexOf("<porom"));
                -1 == c && (c = a.indexOf("<POROM"));
                if (-1 != c) {
                    for (var a = a.substring(c), c = a.indexOf(">"), d = a.substring(0, c + 1), a = a.substring(c), e = "", c = d.indexOf("name="); '"' != d.charAt(c);)
                        c++;
                    for (c++; '"' != d.charAt(c);)e += d.charAt(c++);
                    for (var g = "", c = d.indexOf("value="); '"' != d.charAt(c);)
                        c++;
                    for (c++; '"' != d.charAt(c);)
                        g += d.charAt(c++);
                    switch (e) {
                        case "p1":
                            e = "problem";
                            g = "\n" + g;
                            break;
                        case "s1":
                            e = "solution";
                            g = "\n" + g;
                            break;
                        case "m1":
                            e = "moves";
                            g = "\n" + g;
                            break;
                        case "a1":
                            e = "areas";
                            g = "\n" + g;
                            break;
                        case "g1":
                            e = "clues";
                            g = "\n" + g;
                            break;
                        case "r1":
                            e = "rlabels";
                            g = "\n" + g;
                            break;
                        case "c1":
                            e = "clabels";
                            g = "\n" + g;
                            break;
                        case "n1":
                            e = "nodes";
                            g = "\n" + g;
                            break;
                        case "w1":
                            e = "lines", g = "\n" + g
                    }
                    b = this.keys.contains(e) ? b + (e + " " + g + "\n") : b + (g + "\n")
                }
            }
            t = b
        }
        catch (f) {
            throw this.exception(f), f;
        }
    };
    this.readData = function () {
        try {
            for (var a = null, b = 0, c = t.split(/[\r\n\uffff]+/), d = "", e = 0; e < c.length; e++)
                if (!c[e].startsWith(";") && !(c[e].startsWith("//") || 0 == c[e].trim().length)) {
                    var g = c[e].indexOf(" "), f = "", k = "";
                    -1 == g ? f = c[e] : (f = c[e].substring(0, g), k = c[e].substring(g + 1));
                    f = f.trim();
                    if ("begin" == f) {
                        null == a && (a = this.level);
                        this.level = {};
                        for (g = 0; g < this.keys.length; g++)
                            a[this.keys[g]] && (this.level[this.keys[g]] = a[this.keys[g]]);
                        this.level.nr = b
                    }
                    else"end" == f ? !this.level.nr && null == a ? a = this.level : (this.levels.push(this.level), b++) : this.keys.contains(f) ? (k = k.trim(), this.level[f] = k, d = f) : (0 != this.level[d].length && (this.level[d] += "\n"), this.level[d] += c[e])
                }
        }
        catch (m) {
            throw this.exception(m), m;
        }
    };
    this.select = function (a) {
        try {
            ojdebug("select:", a), 0 != this.levels.length && (0 > a && (a = 0), a >= this.levels.length && (a = this.levels.length - 1), this.level = this.levels[a], this.setup())
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.setup = function () {
        try {
            this.level.pid || (this.level.pid = 1 >= this.levels.length ? "0" : (this.level.nr + 1).toString());
            this.level.check || (this.level.check = this.checking.rules);
            this.level.variant || (this.level.variant = "");
            this.level.layout || (this.level.layout = "");
            this.level.options || (this.level.options = "");
            this.size.x = this.level.cols ? parseInt(this.level.cols) : this.level.size ? parseInt(this.level.size) : 10;
            this.size.y = this.level.rows ? parseInt(this.level.rows) : this.level.size ? parseInt(this.level.size) : 10;
            this.size.z = this.level.depth ? parseInt(this.level.depth) : this.level.size ? parseInt(this.level.size) : this.size.x == this.size.y ? this.size.x : 10;
            this.setup2();
            this.size.x += this.labels.west + this.labels.east;
            this.size.y += this.labels.north + this.labels.south;
            for (var a = this.board.a.length = this.board.l.length = this.board.c.length = this.board.h.length = this.board.v.length = this.board.n.length = 0, b = 0, c = 0; c < this.size.x; c++) {
                this.board.c[c] = [];
                for (var d = 0; d < this.size.y; d++)
                    this.board.a[b++] = this.board.c[c][d] = new h(c, d, this.item.cell)
            }
            for (c = 0; c < this.size.x; c++) {
                this.board.h[c] = [];
                for (d = 0; d < this.size.y + 1; d++)
                    this.board.a[b++] = this.board.l[a++] = this.board.h[c][d] = new h(c, d, this.item.hline)
            }
            for (c = 0; c < this.size.x + 1; c++) {
                this.board.v[c] = [];
                for (d = 0; d < this.size.y; d++)
                    this.board.a[b++] = this.board.l[a++] = this.board.v[c][d] = new h(c, d, this.item.vline)
            }
            for (c = 0; c < this.size.x + 1; c++) {
                this.board.n[c] = [];
                for (d = 0; d < this.size.y + 1; d++)
                    this.board.a[b++] = this.board.n[c][d] = new h(c, d, this.item.node)
            }
            this.moves.list = [];
            this.moves.current = -1;
            this.moves.last = -1;
            this.moves.disable = 0;
            this.checking.disable = 0;
            this.autoValueMarkers = this.editValueMarkers = !1;
            this.score.best = 0;
            this.score.high = this.level.score ? parseInt(this.level.score.trim()) : 0;
            this.savedGames = [];
            this.level.seed && this.random.init(parseInt(this.level.seed.ltrim("0")));
            (this.level.seed || this.config.mode == this.config.modeGame) && this.make();
            this.timer.start();
            this.server.timingSent = !1;
            this.onSetup();
            this.reset();
            if (this.config.mode == this.config.task) {
                var e = this.storage.getSession(this.config.documentName + "|" + this.level.pid);
                e && (this.movesFromString(e), this.check())
            }
        }
        catch (g) {
            throw this.exception(g), g;
        }
    };
    this.setup2 = function () {
    };
    this.reset = function () {
        try {
            for (var a = 0; a < this.board.a.length; a++)
                this.board.a[a].reset();
            this.solved = !1;
            this.result.code = this.result.none;
            this.current.item = null;
            this.display.cursor = !1;
            this.display.errors = !1;
            this.moves.current = -1;
            this.score.current = 0;
            this.reset2();
            var b = this.line.wall;
            this.enable.pedgelines || (b = this.enable.pgridlines ? this.line.grid : this.line.none);
            if (b != this.line.grid) {
                for (var c = 0; c < this.size.x; c++) {
                    var d = this.board.h[c][0];
                    d.value = this.board.c[c][0].areas > this.area.outside ? b : this.line.none;
                    var e = this.board.h[c][this.size.y];
                    e.value = this.board.c[c][this.size.y - 1].areas > this.area.outside ? b : this.line.none;
                    this.enable.pedgelines && (d.fixed = e.fixed = !0)
                }
                for (var g = 0; g < this.size.y; g++) {
                    var f = this.board.v[0][g];
                    f.value = this.board.c[0][g].areas > this.area.outside ? b : this.line.none;
                    var k = this.board.v[this.size.x][g];
                    k.value = this.board.c[this.size.x - 1][g].areas > this.area.outside ? b : this.line.none;
                    this.enable.pedgelines && (f.fixed = k.fixed = !0)
                }
            }
            for (c = 0; c < this.size.x; c++)
                for (g = 0; g < this.size.y; g++) {
                    if (g < this.size.y - 1) {
                        var m = this.board.c[c][g], n = this.board.c[c][g + 1], h = this.board.h[c][g + 1];
                        m.areas <= this.area.outside && n.areas <= this.area.outside ? h.value = this.line.none : m.areas <= this.area.outside || n.areas <= this.area.outside ? h.value = b : m.areas != n.areas && (h.value = this.line.wall)
                    }
                    if (c < this.size.x - 1) {
                        var m = this.board.c[c][g], n = this.board.c[c + 1][g], x = this.board.v[c + 1][g];
                        m.areas <= this.area.outside && n.areas <= this.area.outside ? x.value = this.line.none : m.areas <= this.area.outside || n.areas <= this.area.outside ? x.value = b : m.areas != n.areas && (x.value = this.line.wall)
                    }
                }
            this.check()
        }
        catch (l) {
            throw this.exception(l), l;
        }
    };
    this.reset2 = function () {
    };
    this.reset2lines = function (a, b, c, d, e) {
        try {
            for (var g = 0, f = e.replace(/\s+/g, " ").trim().split(" "); b < d; b++)
                for (e = a; e < c; e++) {
                    var k = 0, m = f[g++];
                    "-" == m || "." == m || (m.match(/^[0-9]+$/) ? k = parseInt(m) : (m.contains("e") && (k += 1), m.contains("s") && (k += 2), m.contains("w") && (k += 4), m.contains("n") && (k += 8)), 0 != (k & 1) && (this.board.v[e + 1][b].value = this.line.wall), 0 != (k & 2) && (this.board.h[e][b + 1].value = this.line.wall), 0 != (k & 4) && (this.board.v[e][b].value = this.line.wall), 0 != (k & 8) && (this.board.h[e][b].value = this.line.wall))
                }
        }
        catch (n) {
            throw this.exception(n), n;
        }
    };
    this.reset2areas = function (a, b, c, d, e) {
        try {
            for (var g = 0, f = e.replace(/\s+/g, " ").trim().split(" "); b < d; b++)
                for (e = a; e < c; e++) {
                    var k = this.board.c[e][b], m = f[g++];
                    "-" == m || "." == m ? k.areas = nil : "@" == m ? k.areas = this.area.outside : "#" == m ? k.areas = this.area.black : "+" == m ? k.areas = this.area.label : "&" == m ? k.areas = this.area.aside : m.match(/^[0-9]+$/) ? k.areas = parseInt(m) : k.areas = m.charCodeAt(0) + 800;
                    k.areas < nil && (k.fixed = !0, k.areas <= this.area.outside && (k.valid = !1))
                }
        }
        catch (n) {
            throw this.exception(n), n;
        }
    };
    this.reset2labels = function (a, b) {
        try {
            void 0 === a && (a = !1);
            void 0 === b && (b = !0);
            for (var c = this.board.c, d = 0; d < this.size.y; ++d)
                for (var e = 0; e < this.size.x; ++e)
                    if (e < this.labels.west || d < this.labels.north || e > this.size.x - this.labels.east - 1 || d > this.size.y - this.labels.south - 1)
                        c[e][d].valid = a, c[e][d].fixed = b, c[e][d].areas = this.area.label
        }
        catch (g) {
            throw this.exception(g), g;
        }
    };
    this.check = function () {
        try {
            if (0 == this.checking.disable) {
                for (var a = 0; a < this.board.a.length; a++) {
                    var b = this.board.a[a];
                    b.work = nil;
                    b.error = b.count = 0;
                    b.checked = b.marked = !1
                }
                this.solved = !0;
                if (this.level.check == this.checking.solution || this.level.check == this.checking.both)
                    this.solved = !this.isNewSolution();
                (this.level.check == this.checking.rules || this.level.check == this.checking.both) && this.check2();
                for (a = 0; a < this.board.a.length; a++)
                    this.board.a[a].error && (this.solved = !1);
                this.solved && (this.server.send(this.server.timing), this.config.mode != this.config.modeGame && (this.cleanSolution(), this.isNewSolution() && this.server.send(this.server.solution, this.solutionToString(!1) + "\n\n" + this.solutionToString(!0) + "\n\nmoves\n" + this.movesToString() + "end\n")))
            }
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.check2 = function () {
        try {
            this.solved = !this.isNewSolution()
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.make = function () {
        try {
            this.overwritten.make2 && this.make2()
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.make2 = function () {
        ojdebug("Make2")
    };
    this.solve = function () {
        try {
            this.overwritten.solve2 && (this.solve2(), this.pushEvent(this.moves.typeSolve, this.current.color), this.check())
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.solve2 = function () {
        ojdebug("Solve2")
    };
    this.isNewSolution = function () {
        try {
            var a = navigator.userAgent;
            return this.level.solution && a.contains("iPhone") && a.contains("iPad") && a.contains("iPod") ? !1 : this.solutionToString(!0) != this.solutionToString()
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.isNewSolutionGame = function () {
        try {
            if (!this.solved || this.result.code == this.result.lost)
                return !1;
            var a;
            a = this.score.optimize == this.score.minimize ? this.score.current < this.score.best : this.score.current > this.score.best;
            if (0 == this.score.best || a)
                this.score.best = this.score.current;
            a = this.score.optimize == this.score.minimize ? this.score.best < this.score.high : this.score.best > this.score.high;
            if (a = 0 == this.score.high || a)this.score.high = this.score.best;
            return a
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.cleanSolution = function () {
    };
    this.showSolution = function () {
        try {
            this.level.solution && (this.solved ? null != this.level.moves && (this.movesFromString(this.level.moves), this.undoAll()) : (this.moves.disable++, this.checking.disable++, this.showSolution2(), this.moves.disable--, this.checking.disable--, this.pushEvent(this.moves.typeShowSolution, this.current.color)), this.server.timingSent = !0, this.current.item = null, this.check())
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.showSolutionGame = function () {
        try {
            this.level.solution && (this.movesFromString(this.level.solution), this.undoAll(), this.server.timingSent = !0, this.check())
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.showSolution2 = function () {
        try {
            for (var a = 0; a < this.size.x; a++)
                for (var b = 0; b < this.size.y; b++) {
                    var c = this.board.c[a][b];
                    c.color = 0;
                    c.solution == nil && c.value == this.cell.nilalias || c.value != c.solution && this.makeMove(c, c.solution, this.current.color)
                }
        }
        catch (d) {
            throw this.exception(d), d;
        }
    };
    this.showHint = function (a) {
        try {
            null != this.level.solution && (a || (a = this.current.item), a && (this.showHint2(a), this.server.timingSent = !0, this.check()))
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.showHint2 = function (a) {
        try {
            ojassert(a, "No item"), a.type == this.item.cell && a.solution == nil ? this.makeMove(a, this.cell.nilalias, this.current.color) : this.makeMove(a, a.solution, this.current.color)
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.makeMove = function (a, b, c, d) {
        try {
            a || (a = this.current.item), null != a && a.valid && (a.type == this.item.cell && this.current.marker != nil && (void 0 === b || null == b) ? this.toggleMarker(this.current.item, this.current.marker) : (a.fixed && (b = a.value), d ? this.makeMove2Alt(a, b, c) : this.makeMove2(a, b, c), this.autoValueMarkers && this.updateValueMarkers(), this.display.errors = !1, this.check()))
        }
        catch (e) {
            throw this.exception(e), e;
        }
    };
    this.makeMove2 = function (a, b, c) {
        try {
            ojassert(a, "No item");
            var d = null;
            a.type == this.item.cell && null != this.cell.values ? d = this.cell.values : a.type >= this.item.line && null != this.line.values ? d = this.line.values : a.type == this.item.node && null != this.node.values && (d = this.node.values);
            if (void 0 === b || null == b)
                if (this.enable.currentValue && a.value != this.current.value && (a.type == this.current.type || a.type >= this.item.line && this.current.type >= this.item.line))
                    b = this.current.value;
                else if (null == d)
                    b = nil;
                else {
                    var e = d.indexOf(a.value), e = -1 == e || e == d.length - 1 ? 0 : e + 1;
                    b = d[e];
                    a.type == this.current.type && (this.enable.currentValue && b == this.current.pvalue && 2 < d.length) && (e = e == d.length - 1 ? 0 : e + 1, b = d[e])
                }
            if (void 0 === c || null == c)c = this.current.color;
            c || (c = 0);
            0 == this.moves.disable && 0 == this.checking.disable && ojdebug("makeMove2: t:", a.type, "x:", a.x, "y:", a.y, "v:", b, "c:", c);
            if ((a.type == this.item.cell && this.cell.min <= this.cell.max && b >= this.cell.min && b <= this.cell.max || null == d || d.contains(b)) && !(a.value == b && a.color == c))
                this.current.pvalue = a.value, a.value = b, a.color = c, a.markers.clear(this.marker.numberBase, this.marker.numberLast), this.current.item = a, this.current.type = a.type, this.current.value = a.value, this.current.color = a.color, this.current.marker = nil, this.pushMove(a)
        }
        catch (g) {
            throw this.exception(g), g;
        }
    };
    this.makeMove2Alt = function (a, b, c) {
        try {
            this.makeMove2(a, b, c)
        }
        catch (d) {
            throw this.exception(d), d;
        }
    };
    this.moveToDxDy = function (a, b) {
        try {
            this.display.cursor = !0;
            if (null == this.current.item || this.current.item.type != this.item.cell)
                for (var c = 0; c < this.size.y; c++)
                    for (var d = 0; d < this.size.x; d++)
                        if (this.board.c[d][c].valid) {
                            this.moveTo(this.board.c[d][c]);
                            return
                        }
            d = this.current.item.x;
            for (c = this.current.item.y; ;) {
                d += a;
                c += b;
                0 > d && (d = this.size.x - 1);
                d == this.size.x && (d = 0);
                0 > c && (c = this.size.y - 1);
                c == this.size.y && (c = 0);
                if (this.board.c[d][c].valid) {
                    this.moveTo(this.board.c[d][c]);
                    break
                }
                if (d == this.current.item.x && c == this.current.item.y)
                    break
            }
        }
        catch (e) {
            throw this.exception(e), e;
        }
    };
    this.moveTo = function (a, b) {
        try {
            this.current.item = a && a.valid ? a : null
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.dragToDxDy = function (a, b, c) {
        try {
            if (this.enable.dragging && null != this.current.item) {
                var d = this.current.item;
                this.moveToDxDy(a, b);
                this.dragTo(this.current.item, d, c)
            }
        }
        catch (e) {
            throw this.exception(e), e;
        }
    };
    this.dragTo = function (a, b, c) {
        try {
            if (this.enable.dragging && (b || (b = this.current.item), b && a && !(b.type == this.item.cell && a.type != this.item.cell || b.type == this.item.node && a.type != this.item.node || b.type > this.item.line && a.type <= this.item.line)))
                this.pointer.dragging || (this.pointer.dragging = !0, this.dragStart(a, b, c)), this.pointer.dragging && (c ? this.dragTo2Alt(a, b) : this.dragTo2(a, b))
        }
        catch (d) {
            throw this.exception(d), d;
        }
    };
    this.dragTo2 = function (a, b) {
        try {
            ojassert(b, "No from item"), ojassert(a, "No to item"), ojassert(b.type == a.type || b.type > this.item.line && a.type > this.item.line, "Type mismatch: " + b.type + ", " + a.type), this.makeMove(a, b.value, this.current.color)
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.dragTo2Alt = function (a, b) {
        this.dragTo2(a, b)
    };
    this.dragStart = function (a, b, c) {
        ojdebug("dragStart: from:", b.type, b.x, b.y, "to:", a.type, a.x, a.y)
    };
    this.dragEnd = function () {
        this.current.item ? ojdebug("dragEnd:   item:", this.current.item.type, this.current.item.x, this.current.item.y) : ojdebug("dragEnd")
    };
    this.pushEvent = function (a, b) {
        try {
            0 == this.moves.disable && (this.moves.current++, this.moves.last = this.moves.current, this.moves.list[this.moves.current] = a + "," + b, this.config.mode == this.config.task && this.storage.setSession(this.config.documentName + "|" + this.level.pid, this.movesToString(!0)))
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.pushMove = function (a, b) {
        try {
            if (a && 0 == this.moves.disable) {
                var c = "";
                b ? c += b : a.type == this.item.cell ? c += this.moves.typeCell : a.type == this.item.hline ? c += this.moves.typeHorizontal : a.type == this.item.vline ? c += this.moves.typeVertical : a.type == this.item.node && (c += this.moves.typeNode);
                var c = c + ("," + a.x + "," + a.y), d = c.length;
                (!this.moves.collapse || -1 == this.moves.current || "," != this.moves.list[this.moves.current].charAt(d) || this.moves.list[this.moves.current].substring(0, d) != c) && this.moves.current++;
                this.moves.last = this.moves.current
                c += "," + a.value + "," + a.color;
                c += "," + a.markers.toString();
                this.moves.list[this.moves.current] = c;
                this.config.mode == this.config.task && this.storage.setSession(this.config.documentName + "|" + this.level.pid, this.movesToString(!0))
            }
        }
        catch (e) {
            throw this.exception(e), e;
        }
    };
    this.undoOne = function () {
        try {
            this.moves.disable++;
            this.checking.disable++;
            var a = this.moves.current;
            this.reset();
            for (var b = 0; b < a; b++)this.redoOne();
            this.moves.disable--;
            this.checking.disable--;
            this.check()
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.redoOne = function () {
        try {
            if (this.moves.current != this.moves.last) {
                this.moves.disable++;
                this.checking.disable++;
                this.moves.current++;
                var a = this.moves.list[this.moves.current].split(","), b = null;
                switch (a[0]) {
                    case this.moves.typeCell:
                        b = this.board.c[parseInt(a[1])][parseInt(a[2])];
                        break;
                    case this.moves.typeHorizontal:
                        b = this.board.h[parseInt(a[1])][parseInt(a[2])];
                        break;
                    case this.moves.typeVertical:
                        b = this.board.v[parseInt(a[1])][parseInt(a[2])];
                        break;
                    case this.moves.typeNode:
                        b = this.board.n[parseInt(a[1])][parseInt(a[2])];
                        break;
                    case this.moves.typeHint:
                        this.showHint(this.board.c[parseInt(a[1])][parseInt(a[2])]);
                        break;
                    case this.moves.typeShowSolution:
                        this.showSolution();
                        break;
                    case this.moves.typeAccept:
                        this.acceptColor(a[1]);
                        break;
                    case this.moves.typeReject:
                        this.rejectColor(a[1]);
                        break;
                    case this.moves.typeSolve:
                        this.current.color = a[1];
                        this.solve();
                        break;
                    case this.moves.typeCheck:
                        this.check();
                        break;
                    case this.moves.typeRemove:
                        this.removeAllMarkers();
                        break;
                    case this.moves.typeInitValueMarkers:
                        this.initValueMarkers();
                        break;
                    case this.moves.typeUpdateValueMarkers:
                        this.updateValueMarkers()
                }
                null != b && (this.makeMove(b, parseInt(a[3]), parseInt(a[4])), b.markers.fromString(a[5]));
                this.moves.disable--;
                this.checking.disable--;
                this.check()
            }
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.undoAll = function () {
        try {
            this.reset(), this.check()
        }
        catch (a) {
            throw this.exception(a), a;
        }
    };
    this.redoAll = function () {
        try {
            this.moves.disable++;
            this.checking.disable++;
            for (var a = this.moves.current; a <= this.moves.last; a++)
                this.redoOne();
            this.moves.disable--;
            this.checking.disable--;
            this.check()
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.loadPuzzle = function (a) {
        try {
            if (0 < a && 9 > a)
                this.savedGames[a] ? (this.movesFromString(this.savedGames[a]), this.redoAll(), this.display.errors = !1, this.check()) : this.paintMessage(this.uis.get("notloaded"));
            else {
                this.paintMessage(this.uis.get("loading"));
                var b = this.server.send(this.server.load);
                if (!b.contains("true\nZ") && !b.contains("false\nZ"))
                    this.paintMessage(this.uis.get("notloaded"));
                else {
                    var c = b.indexOf("\n"), d = b.substring(0, c), e = d.indexOf(" "), g = parseInt(d.substring(0, e));
                    this.timer.setUsedTime(g);
                    d = d.substring(e + 1);
                    e = d.indexOf(" ");
                    g = parseInt(d.substring(0, e));
                    this.timer.setElapsedTime(g);
                    "true" == d.substring(e + 1) ? this.server.timingFeedbackSent = !0 : this.server.timingFeedbackSent = !1;
                    this.movesFromString(b.substring(c + 1));
                    this.redoAll();
                    this.display.errors = !1;
                    this.check();
                    this.paintMessage(this.uis.get("loaded"))
                }
                ojdebug(this.messageText)
            }
        }
        catch (f) {
            throw this.exception(f), f;
        }
    };
    this.savePuzzle = function (a) {
        try {
            if (0 < a && 9 > a)
                this.savedGames[a] = this.movesToString(!0);
            else {
                var b = "" + this.timer.getUsedTime() + " " + this.timer.getElapsedTime() + " " + this.server.timingSent + "\n" + this.movesToString(!0);
                this.paintMessage(this.uis.get("saving"));
                this.server.send(this.server.save, b);
                this.server.send(this.server.load).length == b.length ? this.messageText = this.uis.get("saved") : this.messageText = this.uis.get("notsaved");
                this.paintMessage();
                ojdebug(this.messageText)
            }
        }
        catch (c) {
            throw this.exception(c), c;
        }
    };
    this.movesToString = function (a) {
        try {
            for (var b = "", c = "Z2;", d = 1, e = 0; e < this.moves.current + 1; e++) {
                var g = this.moves.list[e].split(",");
                g[0] != this.moves.typeCell && (c += g[0]);
                g[0] != this.moves.typeCell && g[0] != this.moves.typeNode && g[0] != this.moves.typeVertical && g[0] != this.moves.typeHorizontal ? c += g[1] + ";" : (c = 26 > g[1] && 26 > g[2] ? c + (String.fromCharCode(97 + parseInt(g[1])) + String.fromCharCode(97 + parseInt(g[2])) + ",") : c + (100 * parseInt(g[1]) + parseInt(g[2]) + ","), c = "-1" == g[3] ? c + "-" : c + g[3], c += ",", "0" != g[4] && (c += g[4]), c += ",", "" != g[5] && (c += g[5]), c += ",", c = c.trim(",") + ";");
                50 < c.length && (b = u && !a ? b + ("   <" + u + ' name="m' + d++ + '" value="' + c + '">\n') : b + (c + "\n"), c = "")
            }
            "" != c && (b = u && !a ? b + ("   <" + u + ' name="m' + d++ + '" value="' + c + '">\n') : b + (c + "\n"));
            return b
        }
        catch (f) {
            throw this.exception(f), f;
        }
    };
    this.movesFromString = function (a) {
        try {
            var b = a;
            this.checking.disable++;
            this.undoAll();
            a = a.replace(/\s+/g, "");
            for (var c = a.split(";"), d = 0; d < c.length - 1; d++) {
                var e = c[d].split(","), g = e[0].charAt(0);
                "A" <= g && "Z" >= g ? e[0] = e[0].substring(1) : g = this.moves.typeCell;
                switch (g) {
                    case this.moves.typeVersion:
                        parseInt(e[0]);
                        break;
                    case this.moves.typeAccept:
                        this.acceptColor(parseInt(e[0]));
                        break;
                    case this.moves.typeReject:
                        this.rejectColor(parseInt(e[0]));
                        break;
                    case this.moves.typeRemove:
                        this.removeAllMarkers();
                        break;
                    case this.moves.typeShowSolution:
                        this.showSolution();
                        break;
                    case this.moves.typeSolve:
                        this.solve();
                        break;
                    case this.moves.typeHint:
                        this.showHint();
                        break;
                    case this.moves.typeCheck:
                        this.check();
                        break;
                    case this.moves.typeInitValueMarkers:
                        this.initValueMarkers();
                        break;
                    case this.moves.typeUpdateValueMarkers:
                        this.updateValueMarkers();
                        break;
                    default:
                        var f = a = 0;
                        if ("a" <= e[0].charAt(0) && "z" >= e[0].charAt(0))
                            a = e[0].charCodeAt(0) - 97, f = e[0].charCodeAt(1) - 97;
                        else {
                            var k = parseInt(e[0]);
                            a = Math.floor(k / 100);
                            f = k % 100
                        }
                        var m = nil;
                        void 0 === e[1] || ("" == e[1] || "-" == e[1]) || (m = parseInt(e[1]));
                        var n = e[2] ? parseInt(e[2]) : 0;
                        g == this.moves.typeHorizontal ? this.makeMove(this.board.h[a][f], m, n) : g == this.moves.typeVertical ? this.makeMove(this.board.v[a][f], m, n) : g == this.moves.typeNode ? this.makeMove(this.board.n[a][f], m, n) : ((this.board.c[a][f].value != m || this.board.c[a][f].color != n) && this.makeMove(this.board.c[a][f], m, n), e[3] && 0 != e[3].length && (this.board.c[a][f].markers.fromString(e[3]), this.pushMove(this.board.c[a][f])))
                }
            }
        }
        catch (h) {
            ojdebug("Movelist: " + d + "\n", b), this.exception(h)
        }
        finally {
            this.checking.disable--
        }
    };
    this.setColor = function (a) {
        try {
            this.current.color = a
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.acceptColor = function (a) {
        try {
            if (void 0 === a || null == a)a = this.current.color;
            0 != a && (this.moves.disable++, this.checking.disable++, this.acceptColor2(a), this.moves.disable--, this.checking.disable--, this.pushEvent(this.moves.typeAccept, a), this.check())
        }
        catch (b) {
            throw this.exception(b), b;
        }
    };
    this.acceptColor2 = function (a) {
        try {
            for (var b = 0; b < this.board.a.length; b++) {
                var c = this.board.a[b];
                c.color == a && this.makeMove(c, c.value, 0)
            }
        }
        catch (d) {
            throw this.exception(d), d;
        }
    };
    this.rejectColor = function (a) {
        try {
            if (void 0 === a || null == a)a = this.current.color;
            if (0 != a) {
                this.moves.disable++;
                this.checking.disable++;
                var b = this.current.color;
                this.rejectColor2(a);
                this.current.color = b;
                this.moves.disable--;
                this.checking.disable--;
                this.pushEvent(this.moves.typeReject, a);
                this.check()
            }
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.rejectColor2 = function (a) {
        try {
            for (var b = 0; b < this.board.a.length; b++) {
                var c = this.board.a[b];
                c.color == a && this.makeMove(c, nil, 0)
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.toggleMarkerMode = function () {
        try {
            this.editValueMarkers = this.editValueMarkers ? !1 : !0
        } catch (a) {
            throw this.exception(a), a;
        }
    };
    this.initValueMarkers = function () {
        this.initValueMarkers2();
        this.updateValueMarkers2();
        this.autoValueMarkers || this.pushEvent(this.moves.typeInitValueMarkers, 0)
    };
    this.initValueMarkers2 = function () {
    };
    this.updateValueMarkers = function () {
        this.updateValueMarkers2();
        this.autoValueMarkers || this.pushEvent(this.moves.typeUpdateValueMarkers, 0)
    };
    this.updateValueMarkers2 = function () {
    };
    this.toggleValueMarker = function (a, b) {
        try {
            this.toggleMarker(a, b)
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.toggleMarker = function (a, b) {
        try {
            a || (a = this.current.item), null != a && a.valid && (a.markers.toggle(b),
                this.pushMove(a))
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.removeAllMarkers = function () {
        try {
            for (var a = 0; a < this.board.a.length; a++)this.board.a[a].color = 0, this.board.a[a].markers.clear();
            this.pushEvent(this.moves.typeRemove, 0)
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.numberToString = function (a) {
        try {
            switch (a) {
                case nil:
                    return "-";
                case nil - 1:
                    return "z";
                case nil - 2:
                    return "d";
                case nil - 3:
                    return "v";
                case nil - 4:
                    return "f";
                default:
                    return a.toString()
            }
        } catch (b) {
            return ojdebug(b.toString()), "%"
        }
    };
    this.valueToString =
        function (a, b) {
            try {
                return this.numberToString(a, b)
            } catch (c) {
                return ojdebug(c.toString()), "%"
            }
        };
    this.labelToString = function (a, b) {
        try {
            return this.numberToString(a)
        } catch (c) {
            return ojdebug(c.toString()), "%"
        }
    };
    this.cluesToString = function (a, b) {
        try {
            return this.numberToString(a)
        } catch (c) {
            return ojdebug(c.toString()), "%"
        }
    };
    this.areasToString = function (a, b) {
        try {
            switch (a) {
                case nil:
                    return "-";
                case this.area.outside:
                    return "@";
                case this.area.label:
                    return "+";
                case this.area.aside:
                    return "&";
                case this.area.black:
                    return "#";
                default:
                    return parseInt(a)
            }
        } catch (c) {
            return ojdebug(c.toString()), "%"
        }
    };
    this.solutionToString = function (a) {
        try {
            for (var b = u ? "" : "solution\n", c = this.labels.north; c < this.size.y - this.labels.south; c++) {
                u && (b += "   <" + u + ' name="s' + (c - this.labels.north + 1) + '" value="');
                for (var d = this.labels.west; d < this.size.x - this.labels.east; d++)var e = a ? this.board.c[d][c].solution : this.board.c[d][c].value, b = e == this.cell.nilalias ? b + (this.valueToString(nil) + " ") : b + (this.valueToString(e) + " ");
                b = b.rtrim();
                u && (b += '">');
                b += "\n"
            }
            u ||
            (b += "end\n");
            return b
        } catch (g) {
            throw this.exception(g), g;
        }
    };
    this.solutionToStringGame = function (a) {
        try {
            return a ? "begin\nsolver " + this.level.solver + "\nscore " + this.level.score + "\nsolution\n" + this.level.solution + "end\n" : "begin\nscore " + this.score.current + "\nsolution\n" + this.movesToString() + "end\n"
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.toString = function () {
        try {
            var a = "", b = this.board.c;
            null != this.current.item && (a += "Item: " + this.current.item.x + ", " + this.current.item.y + ", " + this.current.color + "\n");
            for (var a =
                a + ("Size: " + this.size.x + ", " + this.size.y + ", " + this.size.z + "\n"), a = a + "Puzzle:\n", c = 0; c < this.size.y; c++) {
                for (var d = 0; d < this.size.x; d++)var e = b[d][c], a = e.label != nil && (e.value == nil || e.value == this.cell.nilalias) ? a + (this.labelToString(e.label, !0) + " ") : a + (this.valueToString(e.value, !0) + " ");
                a += "\n"
            }
            a += "Values:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.valueToString(b[d][c].value, !0) + " ";
                a += "\n"
            }
            a += "Solution:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.valueToString(b[d][c].solution,
                    !0) + " ";
                a += "\n"
            }
            a += "Labels:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.labelToString(b[d][c].label, !0) + " ";
                a += "\n"
            }
            a += "Clues:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.cluesToString(b[d][c].clues, !0) + " ";
                a += "\n"
            }
            a += "Areas:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.areasToString(b[d][c].areas, !0) + " ";
                a += "\n"
            }
            a += "Errors:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)switch (b[d][c].error) {
                    case 0:
                        a += "- ";
                        break;
                    case -1:
                        a += "e ";
                        break;
                    case -2:
                        a += "z ";
                        break;
                    case -3:
                        a += "d ";
                        break;
                    case -4:
                        a += "v ";
                        break;
                    case -5:
                        a += "f ";
                        break;
                    case -6:
                        a += "s ";
                        break;
                    default:
                        a += parseInt(b[d][c].error) + " "
                }
                a += "\n"
            }
            a += "Marked=1 und Checked=2:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)e = b[d][c], a = e.marked && e.checked ? a + "3 " : e.marked ? a + "1 " : e.checked ? a + "2 " : a + "- ";
                a += "\n"
            }
            a += "Count:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += this.numberToString(b[d][c].count) + " ";
                a += "\n"
            }
            a += "Work:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d <
                this.size.x; d++)a += this.numberToString(b[d][c].work) + " ";
                a += "\n"
            }
            a += "State:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += b[d][c].state + " ";
                a += "\n"
            }
            a += "Colors:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a += b[d][c].color + " ";
                a += "\n"
            }
            a += "Markers:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++) {
                    var g = this.board.c[d][c].markers.toString();
                    "" == g && (g = "-");
                    a += g + " "
                }
                a += "\n"
            }
            a += "Fixed=1 und Invalid=2:\n";
            for (c = 0; c < this.size.y; c++) {
                for (d = 0; d < this.size.x; d++)a = this.board.c[d][c].fixed && !this.board.c[d][c].valid ? a + "3 " : this.board.c[d][c].fixed ? a + "1 " : this.board.c[d][c].valid ? a + "- " : a + "2 ";
                a += "\n"
            }
            a += "Moves:\n";
            for (b = 0; b < this.moves.current + 1; b++)a += this.moves.list[b] + "\n";
            return a
        } catch (f) {
            return f.toString()
        }
    };
    this.uie = {
        value: null,
        color: null,
        smarker: null,
        wmarker: null,
        solution: null,
        check: null,
        hint: null,
        prev: null,
        next: null,
        level: null,
        toolbar: null,
        message: null,
        info: null,
        scroller: null,
        zoomlist: null,
        savelist: null,
        levellist: null
    };
    this.uic = {
        none: "#414243",
        canvas: "#eeeeee",
        label: "#eeeeee",
        edge: "#000000",
        wall: "#000000",
        grid: "#aaaaaa",
        text: "#000000",
        text2: "#ffffff",
        clue: "#3333ff",
        clue2: "#ccccff",
        error: "#ff0000",
        cursor: "#ff0000",
        smarkers: "#776655",
        vmarkers: "#660000",
        lost: "#cc3333",
        draw: "#cccc33",
        won: "#33cc33",
        solved: "#33cc33",
        black: "#333333",
        white: "#ffffff",
        gray: "#cccccc",
        marks: "#000000",
        line: "#aaaaaa",
        hole: "#333333",
        cross: "#666666",
        dark: "#444444 #e00000 #00cc00 #0000e0 #ffcc00 #c00080 #009999 #ff3300 #660099 #99cc00".split(" "),
        light: "#ffffff #ff9999 #66ff99 #9999ff #ffff99 #ff99ff #99ffff #ffcc80 #cc99ff #ccff66".split(" "),
        messagePanel: "#cccccc",
        messageText: "#000000",
        infoPanel: "#ffddff",
        infoText: "#000000",
        toolbarPanel: "#cccccc",
        toolbarText: "#000000",
        buttonBorderDark: "#666666",
        buttonBorderLight: "#ffffff",
        buttonHighlight: "#ffbb77",
        buttonValueFrame: "#ff8888",
        buttonMarkerFrame: "#888888",
        keypadBackground: "#eeeeee",
        keypadBorder: "#cc0000",
        keypadButton: "#dddddd",
        keypadText: "#000000",
        keypadHeader: "#ffbbbb",
        keypadClose: "#ff8888",
        keypadDigits: "#bbffbb"
    };
    (function () {
        this.config.janko && (this.uic.canvas = this.uic.label = this.uic.infoPanel =
            "#e6dcbe", this.uic.toolbarPanel = this.uic.messagePanel = "#ccac85")
    }).apply(this);
    this.uim = {
        grid: 1,
        wall: 3,
        edge: 3,
        cellCursor: 2,
        lineCursor: 1,
        nodeCursor: 2,
        labelCursor: 1,
        margin: 15,
        padding: 1,
        scrollbar: 0,
        buttonBorder: 1,
        buttonPadding: 3,
        buttonSize: 16,
        infoHeight: 25,
        longTouch: 500,
        multikey: 700
    };
    (function () {
        this.config.touchscreen && (this.uim.buttonSize = 20)
    }).apply(this);
    this.uis = {
        lang: 0,
        cc: ["en", "de", "fr", "it"],
        puzzle: ["Puzzle", "R\u00e4tsel", "Enigme", "Enigma"],
        author: ["Author", "Autor", "Createur", "Autore"],
        source: ["Source",
            "Quelle", "Origine", "Origine"],
        title: ["Title", "Titel", "Titre", "Titulo"],
        size: ["Size", "Gr\u00f6\u00dfe", "Dimension", "Dimensioni"],
        score: ["Score", "Punkte", "Score", "Punteggio"],
        moves: ["Moves", "Z\u00fcge", "Coups", "Mosse"],
        level: ["Level", "Level", "Niveau", "Livello"],
        error: ["Error", "Fehler", "Erreur", "Errori"],
        numbers: ["Numbers", "Zahlen", "Nombres", "Numeri"],
        letters: ["Letters", "Buchstaben", "Lettres", "Lettre"],
        colors: ["Colors", "Farben", "Couleurs", "Colori"],
        yes: ["Yes", "Ja", "Oui", "Si"],
        no: ["No", "Nein", "Non", "No"],
        accept: ["Accept", "Annehmen", "Accepter", "Accetta"],
        reject: ["Reject", "Ablehnen", "Rejeter", "Rifiuta"],
        remove: ["Remove", "Entfernen", "Enlever", "Eliminare"],
        cancel: ["Cancel", "Abbrechen", "Annuler", "Cancella"],
        close: ["Close", "Schlie\u00dfen", "Fermer", "Chiudi"],
        start: ["Start", "Start", "Commencer", "Apri"],
        mail: ["Mail", "Mail", "Mail", "Mail"],
        auto: ["Auto"],
        server: ["Server", "Server", "Serveur", "Server"],
        local: ["Local", "Lokal", "Local", "Locale"],
        color0: ["Default", "Standard", "Standard", "Predefinito"],
        color1: ["Red",
            "Rot", "Rouge", "Rosso"],
        color2: ["Green", "Gr\u00fcn", "Vert", "Verde"],
        color3: ["Blue", "Blau", "Bleu", "Blu"],
        color4: ["Yellow", "Gelb", "Jaune", "Giallo"],
        color5: ["Magenta", "Magenta", "Magenta", "Magenta"],
        color6: ["Cyan", "Cyan", "Cyan", "Azurro"],
        color7: ["Orange", "Orange", "Orange", "Arancione"],
        color8: ["Violet", "Violett", "Violet", "Viola"],
        color9: ["Lemon", "Lemon", "Lemon", "Limone"],
        won: ["You won", "Sie haben gewonnen", "Vous avez gagn\u00e9", "Hai vinto"],
        draw: ["Draw", "Unentschieden", "Un Tirage au sort", "Un pareggio"],
        lost: ["You lost", "Sie haben verloren", "Vous avez perdu", "Avete perso"],
        solved: ["You solved the puzzle", "Sie haben das R\u00e4tsel gel\u00f6st", "Vous avez r\u00e9solu le Enigme", "Hai risolto il puzzle"],
        saving: ["Saving the game status...", "Spielstand speichern...", "Sauver le situation du jeu...", "Salvare la situazione di puzzle..."],
        saved: ["Game status saved for 10 days", "Spielstand f\u00fcr 10 Tage gespeichert", "Situation du jeu est sauv\u00e9e dans 10 jours", "Ubicazione del puzzle \u00e8 salvato per 10 giorni"],
        notsaved: ["Error: Game status not saved", "Fehler: Spielstand nicht gespeichert", "Erreur: Situation du jeu ne peut pas \u00eatre \u00e9crit correctement", "Errori: Il ubicazione del puzzle non potrebbe essere scritta"],
        loading: ["Loading the game status...", "Spielstand laden...", "Chargement le situation du jeu...", "Caricamento del ubicazione del puzzle..."],
        loaded: ["Game status loaded", "Spielstand geladen", "Situation du jeu charg\u00e9e correctement", "Ubicazione del puzzle \u00e8 stato caricato correttamente"],
        notloaded: ["Error: Game status not loaded", "Fehler: Spielstand nicht geladen", "Erreur: Situation du jeu ne peut pas \u00eatre lu", "Errori: Ubicazione del puzzle non pu\u00f2 essere riprodotto"],
        solving: ["Searching for solutions...", "Suche nach L\u00f6sungen...", "La recherche de solutione...", "Ricerca di soluzioni..."],
        nosol: ["No solution found", "Keine L\u00f6sung gefunden", "Aucune solution trouv\u00e9e", "Nessuna soluzione trovata"],
        onesol: ["Unique solution found", "Eindeutige L\u00f6sung gefunden",
            "Unique solution trouv\u00e9e", "Unica soluzione trovata"],
        manysol: ["Several solutions found", "Mehrere L\u00f6sungen gefunden", "Plusieurs solutions trouv\u00e9es", "Diverse soluzioni trovate"],
        nocanvas: ["HTML5 Canvas is not supported. Please use a more modern browser.", "HTML5 Canvas ist nicht unterst\u00fctzt. Bitte verwenden sie einen moderneren Browser."],
        nodata: ["No Puzzle Data", "Keine R\u00e4tseldaten"],
        get: function (a) {
            return this[a][this.lang] ? this[a][this.lang] : this[a][0] ? this[a][0] : "*"
        }
    };
    (function () {
        this.uis.lang =
            0;
        var a = navigator.language ? navigator.language : navigator.userLanguage;
        if (!(2 > a.length))for (var a = a.substring(0, 2), b = 0; b < this.uis.cc.length; b++)this.uis.cc[b] == a && (this.uis.lang = b)
    }).apply(this);
    this.icons = {
        prev: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAA5UlEQVQ4jbWRsQ2DMBBF2YfUQEPvAZBYwBK0LsMEFEDhxhIFHS0SlheIsoE9BGP8FNEhEgIERTnpl//dv3+e96+xzsI6i1ZLWGdx2qzNCG1GlH0BbcbzgPtk0GqJNE/OAayzGFyH+2QwuO57AN1MZgKwLEYj65VeeqGbl2YClH2BVstZZV+sU22Zl6puV1S3K4TiiFiwBrRabprKvoBQHEJxpHmCS+ive6HGheKzkTYuzSyLPwMoCUFoK8tiRCyYdQn9bQAlWW6MWACh+P4X3qeR9XHco2lk/RuAzvkJ4HnPYvfufQCnTlXz2NZfuAAAAABJRU5ErkJggg==",
        next: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAA7UlEQVQ4jbWSMQqDMBiFvZWLezsFCh7AOYKr5AYOgiI6CHZwVEKy5AgurhZ6DY/wOv2hWqVVaOAtIe97eT+/4/zrKCPR9g2mx4RTgLZv0PYNlJHnIG3foOxSlF16DkIA/bx/hygjbVpeZVZll2KcNYpBoOzS/ZlQX/28b6oYBBIVLyALEAHGWWOc9S4gqgMkKv6sQ33JXAzCKlGxNUd1AJ8zhIJDGbkNeE9by2MuPOZu/yAU3D7wmIvr7QKfM5tKd5uDVEYupp9XGULBEQpuzT5nyKvs910gCCUfMq8BeZUd30Sqspj2kTM9pp/ML2QzWC+nd1h1AAAAAElFTkSuQmCC",
        make: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAALUlEQVQ4jWNgoCL4TwATNgAXINYQvAYgGUSRC/AagtMALIaNGjCMDSABDyIAALE3mHYa638gAAAAAElFTkSuQmCC",
        reset: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAA8klEQVQ4jZ1TQY3EMAysVBT5B0Qp5F8IJhEGxRAChRAMIWAQJjH3GFn15dJbaS1ZaSJ7PPa42/ZiZoAq/S3mX7tv4DiA8/wSpHcgJWDfCXTfH0DMgNYAEaBWVnaAfee3CNA7YDaBqTK5FCBnekx2zxm4rgmgd1LMmTTN6K3xzZNFgDEWbXivKZFeHKK/t7agvQKIg1LlPYJ6fK0P220M0ltRXO2BCFsqJbDyvqMi18UZlPIbpNYFQDRn5MObF+kVQPWpGqVLicHnyVOEcX8UUeVwZv1ToszurX3YyDFYbdXCq5SzmT1sjuPLn8mMO7Dc/WA//wOU3LDynl0AAAAASUVORK5CYII=",
        load: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAVklEQVQ4jc1QQQoAIAjz6f58HcIolawdosEIq41NkUfAREqczZSZTxQuTlzDXwCCjuUxY+5o4t1ZGNQmVwmKGqFWEKvWdEvkxSMBKxbrwoqHwenC/kMDG1/vNSTTTiEAAAAASUVORK5CYII=",
        save: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAQElEQVQ4jWNgoBL4TyZGGPD/P6YgHsuQabIMoMwF2NQOFwOQJHBiNHWYBhCLyXYBJV6gOAxoawADMX7HYyj5AAA0H9cpzICgAAAAAABJRU5ErkJggg==",
        undoall: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAA0ElEQVQ4jZ2ToQ3DMBREvUrKPERZJEuBXSHM2SDU1LCSSUEWqIILQgMLQzKDXRIp8AoqV27847o9+O/u6X/JZowxBkIsoSgDANJY6H6BNDYJAAChHA24jo/Y3JSlsSjbmQZ0wxqbOZnwBArg1+6GdX8DoRwJCMu6XyCUw1He8gB+ngUo2xnS2LfpFZalsfmAcO49oRwOzQ+ArfcXwPu8vuPQvAD8dIkBvJ4gFGF+ZMY0oGxnFNU5+RJ5PcUZf0JRaRSV/voXogwI7QHCfCqTrScWmPRb7OhEYAAAAABJRU5ErkJggg==",
        undo: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAhUlEQVQ4jWNgIBL8hwJi1WNojpvyijwDYJpdy86SbgBM89K9/0k3AFlz8RISDUDXbFf/gXgDYJrJMgBZ8xyo5rgpr/7b1X/4b5y0ljQXkG0AzBDXsrNw58ukfybNAJghmsnn4AZoBs0hLx1oJh8j3wBklyh6TaEsLyh69ZBvAMwQigzABQBdtfzw+O8tkgAAAABJRU5ErkJggg==",
        redo: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAqUlEQVQ4jaXTIQ7CMBTG8R0DuwMgJmu3W/QCCJKZqnlkRQ9Qi0RO7grICURvsCAmkH/E9ghZCGm7Tzb5fnmvySuKTVizfY8OQOunfEQAbUMeIoAfyENgKfoBXA9Nl4gI4Pp1FTejzvd4RIDL7Yl2M5V5cdAjlb7GIf+AKASWvVs/fcplbSlrGz/BLyDpD5ouoG1ILwugzIgyGeVvIKsswPH02HcLu64xNW+fvPdZssMHfAAAAABJRU5ErkJggg==",
        redoall: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAA0ElEQVQ4jaXTIQ7DIBQGYK6CaTK57AZPVpEdgaQnwM5hUU3lZO1k/Y6A7AHwrAr5avbIWihd02ff/38BEhhjjOF3WGEwM4tl005FxHuPTTvho/+kWQKEdpsIAf07pDkCssujQDcEBGUThIDsnoBuCPGO69AuILSL5asKWMkRb/IVg977mDkEEPI3QGUOBjmY5ARNOy1OVgTWb1AEQFkU2mXLBICyZQCUzZZ/AaEdXu7PPLBVJqCSIwrtkNddClRy3P0LoCzy2iCvTQqc+o1nZgZ1Uu5EUaoa5AAAAABJRU5ErkJggg==",
        cmarker: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAV0lEQVQ4ja3TuQ0AIBADQfdfFZ2ZAInfYJ6THO5kB+hjN/sIgOzmQkMooLt4hdixQp4AIpTtw1AtIQ2goDY0gLxp+BlYI0b8BdCIGWvkIC4IZsDlV+7CCM80OJoO8o05AAAAAElFTkSuQmCC",
        vmarker: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAKElEQVQ4jWNgoBL4j4RJFYNI/P//H0MxkWLUccHAg9FApAIYDUQKAACqJmuV/ynnFwAAAABJRU5ErkJggg==",
        hint: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAiklEQVQ4ja2SwREAIQgDU3pKs7Pcw0ERQe8hM3w0CwEFAJAQSWGGikTXUyS83i66UNqztSYAOeg7Z3AsEroO60c4KzLYk/UISyhH+QUXY0wHJqzgzUF8PhNGyMPJ/paDS2fmz+iWInIvYmMGbWHl8hMLZi3QO0v923Lf/CkcMPLW8a0DK4Ji/qfxAYfNU4hq9HRHAAAAAElFTkSuQmCC",
        solution: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAeklEQVQ4jdWSQQ7EMAgD/XQ/jZ9NDy0VaUOqzW0t+QQeGSXSJdtoV7aJCHYhWAZoIbZJLwHAsJSh2awFZIsaPKUEpOcAAElExB2sDQAsD5APwNhgA/A3DSrk1wYvSAU8nq4FDKfUQH7z2mgJuINXo84t4LHw5ZeWw5kO20TKocy4Mz0AAAAASUVORK5CYII=",
        check: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAASElEQVQ4jWNgGJLgPwPD//8MDP8hTBJAQ0MDeRop1ky2k6mmGa8B+PxGtO0wQ5AVE2U7LueSrBmfISQZQJbTqW4AzBCyNZMKACZuYqTvRyIAAAAAAElFTkSuQmCC",
        tilt: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAwklEQVQ4jZVSsQ0EIQxjBQrWYIHMQZOBbgq2idjhN7mCwl8ZAbqcDqQUWIljbEJwjllDShGqBV6Pe8waVAtqvaBazkg4bNYAAL33QfSJQLUgpYhaL/TeYdYgkiGSv6tQLRDJY3tKEWbNJ+AWyuSdBNy+9y1vpnSRPNyfFRAXyasnNIzNLGL3/XvERzrcdFIAhrLAvPkUOj6nsONz1Et0dNtLgX3L8BwdQS+Fvc+N9CmF459It+n48U/cTXyV7ZGw3ob/E4mGuuqn2pkAAAAASUVORK5CYII=",
        zoom: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAYElEQVQ4jc2SUQrAMAhD39Fzc/ezgnOLLaODBfyJmCZW2A1JAVzq5JYQQFQksX5Y0m14IDnztp9erZyLY20b3gtQFliFvhd4FWHHEhlNh/Ybs0gXJ5XH5JSXr3Lq8j8iB1I9PeOX61R8AAAAAElFTkSuQmCC",
        info: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAc0lEQVQ4jb2SQQ7AIAgE9+k8bX9GDy3GIoumh07ixbgDRICEmbk6+W0ZJOkKKVJBkuU9AF8EFcB9WoEK7xiSXfWqgxCYmbcd/CNQY8wjZEmEW0HHq/puF2ZIrtUTUvJ829FaeyU6DY9xQtTOfSr6LJiQggujdUSibKeA7QAAAABJRU5ErkJggg=="
    };
    this.css =
    {
        puzzle: "text-align: center; padding: 0px 0px 0px 0px; margin: 0px 0px 0px 0px; border: 0; border-width: 0; border-collapse: collapse; -webkit-user-select: none; -khtml-user-select: none; -moz-user-select: none; -o-user-select: none; user-select: none;",
        icon: "padding: 4px 4px 4px 4px;",
        toolbar: "text-align: center; padding: 4px 8px 0px 8px;",
        infoline: "text-align: center; padding: 2px;",
        msgline: "text-align: center; padding: 2px;"
    };
    this.infoText = this.messageText = this.canvas = null;
    this.keypad = new function () {
        var a =
            null, b = null, c = null, d = null, e = null, g = 4, r = 30, k = 0, m = 0, h = !1, l = [];
        this.header = [["?", 0, f.uic.keypadHeader], ["F", 1, f.uic.keypadHeader], ["M", 2, f.uic.keypadHeader], ["\u00d7", 3, f.uic.keypadClose]];
        this.numbers = [["1", 1], ["2", 2], ["3", 3], ["4", 4], ["5", 5], ["6", 6], ["7", 7], ["8", 8], ["9", 9], ["0", 0], ["...", 10, f.uic.keypadDigits], ["\u2022", 11, f.uic.keypadDigits]];
        this.letters = [["A", 1], ["B", 2], ["C", 3], ["D", 4], ["E", 5], ["F", 6], ["G", 7], ["H", 8], ["I", 9], ["J", 10], ["K", 11], ["L", 12], ["M", 13], ["N", 14], ["O", 15], ["P", 16], ["Q", 17],
            ["R", 18], ["S", 19], ["T", 20], ["U", 21], ["V", 22], ["W", 23], ["X", 24], ["Y", 25], ["Z", 26], ["\u2022", -1], ["\u00d7", 99]];
        this.colors = [["0", 0, f.uic.light[0]], ["1", 1, f.uic.light[1]], ["2", 2, f.uic.light[2]], ["3", 3, f.uic.light[3]], ["4", 4, f.uic.light[4]], ["5", 5, f.uic.light[5]], ["6", 6, f.uic.light[6]], ["7", 7, f.uic.light[7]], ["8", 8, f.uic.light[8]], ["9", 9, f.uic.light[9]], ["+", 10, f.uic.keypadDigits], ["\u2013", 11, f.uic.keypadDigits]];
        this.markers = [[f.paintCircle, f.marker.circle], [f.paintSquare, f.marker.square], [f.paintDot,
            f.marker.dot], [f.paintDecagon, f.marker.decagon], ["a", f.marker.letterA], ["b", f.marker.letterB], ["c", f.marker.letterC], ["d", f.marker.letterD], [f.paintCross, f.marker.cross], [" ", 98], ["\uffff", 98, f.uic.keypadDigits], ["\u00d7", 99, f.uic.keypadDigits]];
        this.show = function (e, p, q) {
            try {
                h = q == this.numbers;
                a = e ? e : 0;
                b = p ? p : null;
                c = q ? q : l;
                f.hidePopups();
                0 == a && (g = Math.ceil(c.length / 4) + 1);
                r = f.config.touchscreen ? 35 : 25;
                4 < g && (r = Math.ceil(5 * r / g));
                var s = document.body;
                null == d && (d = document.createElement("canvas"), d.style.display =
                    "none", s.appendChild(d));
                if (null != b) {
                    e = 4 * r + 4;
                    var t = f.size.x * f.unit.x - e, u = f.size.y * f.unit.y - e;
                    k = (b.x + 1) * f.unit.x;
                    m = (b.y + 1) * f.unit.y;
                    k > t && (k = k - e - f.unit.x);
                    m > u && (m = m - e - f.unit.y);
                    var v = f.getElementPosition(f.canvas);
                    k = v.left + f.base.x + k;
                    m = v.top + f.base.y + m
                } else v = f.getElementPosition(document.getElementById([f.config.appid + "value", f.config.appid + "cmarker", f.config.appid + "smarker"][a])), k = v.left, m = v.top + r;
                d.style.zindex = 2;
                d.style.position = "absolute";
                d.style.left = k + "px";
                d.style.top = m + "px";
                d.style.display =
                    "inline";
                d.width = 4 * r + 5;
                d.height = Math.max(g, 4) * r + 5;
                d.addEvent("mousedown", this.onIgnore.bind(this));
                d.addEvent("mousemove", this.onIgnore.bind(this));
                d.addEvent("mouseup", this.onIgnore.bind(this));
                d.addEvent("click", this.onClick.bind(this));
                d.addEvent("touchstart", this.onClick.bind(this));
                d.addEvent("touchmove", this.onIgnore.bind(this));
                d.addEvent("touchend", this.onIgnore.bind(this));
                d.addEvent("contextmenu", this.onIgnore.bind(this));
                this.paint()
            } catch (w) {
                throw f.exception(w), w;
            }
        };
        this.paint = function () {
            try {
                var b =
                    d.getContext("2d");
                b.fillStyle = f.uic.keypadBackground;
                b.strokeStyle = f.uic.keypadBorder;
                b.lineWidth = 3;
                b.lineCap = "round";
                b.beginPath();
                b.rect(1.5, 1.5, 4 * r + 2, Math.max(g, 4) * r + 2);
                b.fill();
                b.stroke();
                e = 0 == a ? this.header.concat(c) : 1 == a && f.enable.colors ? this.header.concat(this.colors) : 2 == a && f.enable.smarkers ? this.header.concat(this.markers) : this.header;
                b.textAlign = "center";
                b.textBaseline = "middle";
                b.font = Math.floor(2 * r / 3) + "px sans-serif";
                for (var k = 0; k < e.length; k++) {
                    var m = k % 4 * r + 2.5, h = Math.floor(k / 4) * r + 2.5, n =
                        r - 1.5;
                    b.fillStyle = e[k][2] ? e[k][2] : f.uic.keypadButton;
                    b.fillRect(m, h, n, n);
                    var l = {x: m, y: h, w: n, h: n, scale: 60};
                    null != e[k][0] && ("function" === typeof e[k][0] ? e[k][0].call(f, b, l) : "\uffff" == e[k][0] ? (f.paintCircle(b, l), f.paintDot(b, l)) : f.paintCaption(e[k][0], b, {
                        x: m,
                        y: h,
                        w: n,
                        h: n,
                        scale: 80,
                        fill: f.uic.keypadText,
                        stroke: f.uic.keypadText
                    }))
                }
            } catch (p) {
                throw f.exception(p), p;
            }
        };
        this.hide = function () {
            try {
                null != d && (d.style.display = "none")
            } catch (a) {
                throw f.exception(a), a;
            }
        };
        this.onIgnore = function (a) {
            a = a || window.event;
            f.cancelEvent(a)
        };
        this.onClick = function (g) {
            try {
                g = g || window.event;
                var k = d.getBoundingClientRect(), m = 0, l = 0;
                g.clientX ? (m = g.clientX - k.left, l = g.clientY - k.top) : (m = g.touches[0].clientX - k.left, l = g.touches[0].clientY - k.top);
                m = Math.floor(m / r);
                l = Math.floor(l / r);
                k = 4 * l + m;
                if (3 > k)a = k, this.paint(); else if (3 == k)this.hide(); else if (e[k] && null != e[k][1])if (0 == a && h)10 == e[k][1] ? (c[11][0] = "\u2022" == c[11][0] ? "?" : "\u2022", this.paint()) : 11 == e[k][1] ? "?" == c[11][0] || c[11][1] < f.cell.min || c[11][1] > f.cell.max ? (c[11][0] = "?", this.paint()) : ("\u2022" ==
                c[11][0] ? f.onValues2.call(f, b, nil) : "?" != c[11][0] && f.onValues2.call(f, b, parseInt(c[11][0])), c[11][0] = "\u2022", f.paint(), this.hide()) : "\u2022" != c[11][0] ? (c[11][0] = "?" == c[11][0] ? e[k][1] : 10 * c[11][0] + e[k][1], c[11][0] > f.cell.max && (c[11][0] = "?"), this.paint()) : (e[k][1] >= f.cell.min && e[k][1] <= f.cell.max && (f.onValues2.call(f, b, e[k][1]), f.paint()), this.hide()); else {
                    switch (a) {
                        case 0:
                            f.onValues2.call(f, b, e[k][1]);
                            break;
                        case 1:
                            f.onCMarkers2.call(f, b, e[k][1]);
                            break;
                        case 2:
                            f.onSMarkers2.call(f, b, e[k][1])
                    }
                    this.hide();
                    f.paint()
                }
            } catch (p) {
                f.exception(p)
            } finally {
                f.cancelEvent(g)
            }
        }
    };
    this.keypadValues = null;
    this.base = {x: 0, y: 0};
    this.unit = {x: 0, y: 0, min: 15, max: 999};
    this.zoom = {x: 0, y: 0, auto: !1};
    this.pointer = {
        item: nil,
        x: nil,
        y: nil,
        button: 0,
        zooming: !1,
        dragging: !1,
        scrolling: !1,
        cancel: !1,
        magic: 0
    };
    this.display = {cursor: !1, errors: !1};
    this.tilt = {active: !1, beta: !0, gamma: !0, reset: 10, action: 20};
    this.paintToImage = !1;
    this.imageNumber = 1;
    this.charToValue = [];
    this.codeToValue = [8, nil, 46, nil];
    this.valueToMarker = [];
    this.onRun = function () {
        try {
            ojdebug("Version:      ",
                this.userAgentString);
            ojdebug("Screen Width: ", screen.width, screen.availWidth);
            ojdebug("Screen Height:", screen.height, screen.availHeight);
            ojdebug("Window Width: ", window.outerWidth, window.innerWidth);
            ojdebug("Window Height:", window.outerHeight, window.innerHeight);
            ojdebug("User Agent:   ", navigator.userAgent);
            ojdebug("Language:     ", navigator.language, navigator.userLanguage);
            ojdebug("Browser:      ", navigator.appName);
            ojdebug("Code Name:    ", navigator.appCodeName);
            ojdebug("Version:      ", navigator.appVersion);
            ojdebug("Platform:     ", navigator.platform);
            ojdebug("Mobile:       ", this.config.mobile);
            ojdebug("Touchscreen:  ", this.config.touchscreen);
            ojdebug("DB.Local:     ", this.storage.isLocal);
            ojdebug("DB.Indexed:   ", this.storage.isIndexed);
            ojdebug("DB.Session:   ", this.storage.isSession);
            ojdebug("Cookies:      ", this.storage.isCookies);
            ojdebug("Gelocation:   ", !!navigator.geolocation);
            for (var a = [["prev", "$", this.onPrev, this.enable.prevnext], ["level", "@", this.onLevel, this.enable.prevnext], ["next", "$",
                this.onNext, this.enable.prevnext], ["make", "$", this.onMake, this.enable.make], ["reset", "$", this.onReset, this.enable.reset], ["load", "$", this.onLoad, this.enable.loadsave], ["save", "$", this.onSave, this.enable.loadsave], ["undoall", "$", this.onUndoAll, this.enable.undoredo], ["undo", "$", this.onUndoOne, this.enable.undoredo], ["redo", "$", this.onRedoOne, this.enable.undoredo], ["redoall", "$", this.onRedoAll, this.enable.undoredo], ["cmarker", "$", this.onCMarkers, this.enable.colors], ["smarker", "@", this.onSMarkers, this.enable.smarkers],
                ["value", "@", this.onValues, this.enable.current], ["vmarker", "$", this.onVMarkers, this.enable.vmarkers && !this.config.touchscreen], ["hint", "$", this.onHint, this.enable.hint], ["solution", "$", this.onSolution, this.enable.solution], ["check", "$", this.onCheck, this.enable.check], ["tilt", "$", this.onTilt, this.enable.tilt && this.config.mobile], ["zoom", "$", this.onZoom, this.enable.zoom], ["info", "$", this.onInfo, this.enable.info]], b = "\n", c = this.config.appid, d = 'width="' + this.uim.buttonSize + '" height="' + this.uim.buttonSize +
                '" ', b = b + ('<div id="' + c + 'container">\n'), b = b + ('<table id="' + c + 'puzzle" style="' + this.css.puzzle + '">\n'), b = b + " <tr>\n", b = b + ('  <td id="' + c + 'toolbar" style="' + this.css.toolbar + '">\n'), e = 0; e < a.length; e++)"@" == a[e][1] ? b += '   <canvas id="' + c + a[e][0] + '" style="' + this.css.icon + '" ' + d + "></canvas>\n" : "#" == a[e][1] ? b += '   <select id="' + c + a[e][0] + '" style="position: relative; top: -6px;"></select>\n' : (b += '   <img id="' + c + a[e][0] + '" style="' + this.css.icon + '" ', b += 'src="' + this.icons[a[e][0]] + '" ' + d + ">\n");
            b += "  </td>\n";
            b += " </tr>\n";
            b += " <tr>\n";
            b += '  <td id="' + c + 'info-line" style="' + this.css.infoline + '">Info-Line</td>\n';
            b += " </tr>\n";
            b += " <tr>\n";
            b += '  <td id="' + c + 'canvas-cell" style="' + this.css.puzzle + 'text-align: center;">\n';
            b += '   <div id="' + c + 'canvas-scroller" style="' + this.css.puzzle + 'text-align: center; overflow: auto;">\n';
            b += '    <canvas id="' + c + 'canvas" width="305" height="305" style="' + this.css.puzzle + "margin: " + this.uim.margin + 'px;"></canvas>\n';
            b += "   </div>\n";
            b += "  </td>\n";
            b += " </tr>\n";
            b += " <tr>\n";
            b += '  <td id="' + c + 'message-line" style="' + this.css.msgline + '">&nbsp;</td>\n';
            b += " </tr>\n";
            b += "</table>\n";
            b += '<select id="' + c + 'level-list" size="10" style="display: none;">';
            b += "</select>\n";
            b += '<select id="' + c + 'save-list" size="10" style="display: none;">';
            b += "</select>\n";
            b += '<select id="' + c + 'zoom-list" size="10" style="display: none;">';
            b += "</select>\n";
            b += "</div>\n";
            this.config.elem ? document.getElementById(this.config.elem).innerHTML = b : document.write(b);
            for (e = 0; e < a.length; e++) {
                var g = document.getElementById(c +
                a[e][0]);
                g && (g.addEvent("mouseover", this.onButtonOver), g.addEvent("mouseout", this.onButtonOut), g.addEvent("mousedown", this.onButtonDown), g.addEvent("mouseup", this.onButtonUp), g.addEvent("touchstart", this.onButtonDown), g.addEvent("touchend", this.onButtonUp), g.addEvent("touchmove", this.onButtonOver), g.addEvent("contextmenu", this.onContextMenu.bind(this)), g.ojfunction = a[e][2], a[e][3] || (g.style.display = "none"), this.uie[a[e][0]] = g)
            }
            this.uie.info = document.getElementById(c + "info-line");
            this.uie.toolbar =
                document.getElementById(c + "toolbar");
            this.uie.message = document.getElementById(c + "message-line");
            this.uie.zoomlist = document.getElementById(c + "zoom-list");
            this.uie.savelist = document.getElementById(c + "save-list");
            this.uie.levellist = document.getElementById(c + "level-list");
            this.uie.scroller = document.getElementById(c + "canvas-scroller");
            this.uie.toolbar.style.color = this.uic.toolbarText;
            this.uie.toolbar.style.background = this.uic.toolbarPanel;
            this.uie.message.style.color = this.uic.messageText;
            this.uie.message.style.background =
                this.uic.messagePanel;
            this.uie.info.style.color = this.uic.infoText;
            this.uie.info.style.background = this.uic.infoPanel;
            this.uie.value.style.background = "#ff8888";
            this.uie.smarker.style.background = "#888888";
            document.addEvent("keypress", this.onKeyPress.bind(this));
            document.addEvent("keydown", this.onKeyDown.bind(this));
            document.addEvent("keyup", this.onKeyUp.bind(this));
            window.addEvent("resize", this.paint.bind(this));
            window.addEvent("deviceorientation", this.onDeviceOrientation.bind(this));
            if (this.canvas =
                    document.getElementById(c + "canvas"))this.canvas.addEvent("touchstart", this.onTouchStart.bind(this)), this.canvas.addEvent("touchend", this.onTouchEnd.bind(this)), this.canvas.addEvent("touchmove", this.onTouchMove.bind(this)), this.canvas.addEvent("mouseup", this.onMouseUp.bind(this)), this.canvas.addEvent("mousemove", this.onMouseMove.bind(this)), this.canvas.addEvent("mousedown", this.onMouseDown.bind(this)), this.canvas.addEvent("mouseout", this.onMouseOut.bind(this)), this.canvas.addEvent("mousewheel", this.onMouseWheel.bind(this)),
                this.canvas.addEvent("contextmenu", this.onContextMenu.bind(this));
            var f = document.createElement("div");
            f.style.width = f.style.height = "100px";
            f.style.overflow = "scroll";
            f.style.position = "absolute";
            f.style.top = "-9999px";
            document.body.appendChild(f);
            this.uim.scrollbar = f.offsetWidth - f.clientWidth;
            document.body.removeChild(f)
        } catch (k) {
            throw this.exception(k), k;
        }
    };
    this.onSetup = function () {
        try {
            this.uie.solution.style.display = !this.enable.solution || !this.level.solution ? "none" : "", this.uie.hint.style.display = !this.enable.hint || !this.level.solution ? "none" : "", this.uie.check.style.display = !this.enable.check || this.level.check == this.checking.solution ? "none" : "", this.uie.solution.style.background = this.level.moves ? this.uic.buttonHighlight : this.uic.toolbarPanel, 2 > this.levels.length && (this.uie.prev.style.display = this.uie.next.style.display = this.uie.level.style.display = "none"), this.pointer.zooming = this.pointer.scrolling = this.pointer.dragging = !1, this.zoom.x = this.zoom.y = this.unit.x = this.unit.y = 0, this.config.touchscreen ? this.zoom.auto = !0 : this.level.unit ? (this.zoom.auto = !1, this.zoom.x = this.zoom.y = parseInt(this.level.unit)) : this.zoom.auto = !0, this.base.x = this.base.y = 0
        } catch (a) {
            throw this.exception(a), a;
        }
    };
    this.onDisplayScores = function (a) {
        try {
            a = '<table class="scores">\n';
            a += " <tr>\n  <th>Nr.</th>\n  <th>Rekord von</th>\n  <th>" + this.score.label + "</th>\n </tr>\n";
            for (var b = 0; b < this.levels.length; b++) {
                this.select(b);
                if (0 < this.level.score && this.level.solution)try {
                    this.server.timingSent = !0, this.movesFromString(this.level.solution), this.check(),
                        this.solved ? this.score.high != this.score.current && (a = "<p>ERROR \u2013 INVALID SCORE: " + (b + 1) + "</p>\n" + a) : a = "<p>ERROR \u2013 NOT SOLVED: " + (b + 1) + "</p>\n" + a
                } catch (c) {
                    a = "<p>EXCEPTION: " + (b + 1) + "</p>\n" + a
                }
                a += " <tr>\n  <td>" + (b + 1) + "</td>\n  <td>" + (this.level.solver ? this.level.solver : "-") + "</td>\n  <td>" + (this.level.score ? this.level.score : "-") + "</td>\n </tr>\n"
            }
            new ojpopup(a + "</table>\n");
            this.select(0)
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.onInfo = function (a) {
        try {
            var b = '<div id="infotext">\n', b = b + ("<b><big>" +
                this.uis.get("puzzle") + "</big></b>\n\n"), b = b + ("Version " + this.puzzleVersion + "\n"), b = b + (this.copyrightString + "\n"), b = b + "http://www.janko.at/\n", b = b + "http://www.janko.at/Raetsel/\n", b = b + ("Date:" + document.lastModified + "\n\n"), b = b + "<b><big>R\u00e4tseldaten (Puzzle Data):</big></b>\n\n", b = b + ("Autor:   " + this.level.author + "\n"), b = b + ("Quelle:  " + this.level.source + "\n"), b = b + ("Titel:   " + this.level.title + "\n"), b = b + ("Rechte:  " + this.level.rights + "\n"), b = b + ("L\u00f6ser:   " + this.level.solver + "\n"), b = b + ("Info:    " +
                this.level.info + "\n"), b = b + ("PID:     " + this.level.pid + "\n\n"), b = b + "<b><big>Zeitmessung (Timings):</big></b>\n\n", b = b + ("Netto:   " + this.timer.getUsedTime() + "\n"), b = b + ("Brutto:  " + this.timer.getElapsedTime() + "\n\n"), b = b + ("<b><big>L\u00f6sung (Solution):</big></b>\n\n" + this.solutionToString().replace(/</g, "&lt;").replace(/>/g, "&gt;") + "\n"), b = b + ("<b><big>Zugeliste (Move List):</big></b>\n\nmoves\n" + this.movesToString().replace(/</g, "&lt;").replace(/>/g, "&gt;") + "end\n\n");
            a && (b += "<b><big>Internal Data:</big></b>\n\n" +
            this.toString() + "\n\n", b += "<b><big>Debug Buffer:</big></b>\n\n" + ojdebugBuffer + "\n\n");
            var b = b + "</div>\n", c = this.storage.getCookie(this.config.cookieMail);
            c || (c = "");
            var d = this.storage.getCookie(this.config.cookieName);
            d || (d = "");
            var e = this.config.documentName, e = e.replace("http://", "Feedback: ");
            this.config.janko && (e = e.replace(this.config.documentHost + "/", ""), e = e.replace(".a.htm", ""), e = e.replace(".htm", ""), e = e.replace(/\//g, "."), 0 != this.level.pid && (e += "." + this.level.pid));
            b += "<b><big>Mail an uns (Mail to us):</big></b>\n";
            b += '<form method="POST" action="' + this.config.mailScript + "\" onsubmit=\"document.getElementById('info').innerHTML = document.getElementById('infotext').innerHTML; return true;\">\n";
            b += "Ihr Name oder Ihr Pseudonym (erforderlich):\n";
            b += '<input type="text" name="fromname" style="width: 100%" value="' + d + '" id="fromname">\n\n';
            b += "Ihre Mail-Adresse (nur falls Sie eine Antwort erwarten):\n";
            b += '<input type="text" name="frommail" style="width: 100%" value="' + c + '" id="frommail">\n\n';
            b += "Betreff (erforderlich):\n";
            b += '<input type="text" name="subject" style="width: 100%" value="' + e + '" id="subject">\n\n';
            b += "Nachricht (erforderlich):\n";
            b += '<textarea id="nachricht" name="message" rows="12" cols="70" style="width: 100%"></textarea>\n';
            b += '<textarea id="info" name="info" style="display: none;">?</textarea>\n';
            b += '<input type="submit" value="Absenden" name="B1">';
            new ojpopup(b + "</form>\n\n")
        } catch (g) {
        }
    };
    this.onTilt = function (a) {
        try {
            this.enable.tilt && (this.tilt.active = !this.tilt.active)
        } catch (b) {
            throw this.exception(b),
                b;
        }
    };
    this.onZoom = function (a) {
        try {
            if (this.enable.zoom)if (a) {
                this.zoom.auto = !0;
                this.paint();
                var b = document.getElementById(f.config.appid + "container");
                window.scroll(0, f.getElementPosition(b).top - 5)
            } else {
                this.hidePopups();
                var c = this.getElementPosition(this.uie.zoom), b = this.uie.zoomlist, d = '<option value="0" style="color: red;">' + this.uis.get("auto") + "</option>\n";
                a = "10 15 20 25 30 35 40 45 50 60 80 100".split(" ");
                for (var e = 0; e < a.length; e++)d += '<option value="' + a[e] + '">' + a[e] + "</option>\n";
                b.innerHTML =
                    d;
                b.style.zindex = 2;
                b.style.display = "inline";
                b.style.position = "absolute";
                b.style.left = c.left + "px";
                b.style.top = c.top + this.uie.zoom.height + "px";
                b.onchange = this.onZoom2
            }
        } catch (g) {
            throw this.exception(g), g;
        }
    };
    this.onZoom2 = function () {
        try {
            var a = f.uie.zoomlist;
            a.style.display = "none";
            -1 != a.selectedIndex && (0 == a.selectedIndex ? (f.zoom.auto = !0, f.paint(), a = document.getElementById(f.config.appid + "container"), window.scroll(0, f.getElementPosition(a).top - 5)) : (f.zoom.auto = !1, f.zoom.x = f.zoom.y = parseInt(a.options[a.selectedIndex].value)),
                f.paint())
        } catch (b) {
            throw f.exception(b), b;
        }
    };
    this.onSaveImage = function (a) {
        function b(a) {
            var b = document.createElement("applet");
            b.code = "_Puzzle.class";
            c && (b.codeBase = c);
            b.width = 8;
            b.height = 20;
            var d = document.createElement("param");
            d.name = "base";
            d.value = f.config.documentHref;
            b.appendChild(d);
            d = document.createElement("param");
            d.name = "data";
            d.value = f.canvas.toDataURL("image/png").substring(5);
            b.appendChild(d);
            d = document.createElement("param");
            d.name = "file";
            d.value = a;
            b.appendChild(d);
            f.uie.toolbar.appendChild(b)
        }

        var c = "";
        try {
            if (this.config.documentHref.startsWith("file:")) {
                var d = this.config.documentHref.indexOf("/Raetsel/");
                -1 == d && (d = this.config.documentHref.indexOf("/Spiele/"));
                if (-1 != d)for (var e = this.config.documentHref.substring(d + 9), d = 0; d < e.length; d++)"/" == e.charAt(d) && (c = "../" + c);
                var g = this.uic.label, r = this.uic.canvas;
                this.paintToImage = !0;
                this.uic.label = this.uic.canvas = "#ffffff";
                var k = 1 >= this.levels.length ? "" : (this.level.nr + 1).toString() + ".";
                a.contains("e") && (this.paint(), b(k + this.imageNumber++));
                a.contains("c") &&
                (this.reset(), this.paint(), b(k + "c"));
                a.contains("d") && (this.showSolution(), this.paint(), b(k + "d"));
                this.paintToImage = !1;
                this.uic.label = g;
                this.uic.canvas = r;
                this.paint()
            }
        } catch (m) {
            this.exception(m)
        }
    };
    this.onShiftF9 = function (a) {
    };
    this.onShiftF10 = function (a) {
    };
    this.onOptions = function (a) {
    };
    this.onMake = function (a) {
    };
    this.onHint = function (a) {
        this.enable.hint && this.showHint()
    };
    this.onReset = function (a) {
        this.enable.reset && this.reset()
    };
    this.onUndoOne = function (a) {
        this.enable.undoredo && this.undoOne()
    };
    this.onRedoOne =
        function (a) {
            this.enable.undoredo && this.redoOne()
        };
    this.onUndoAll = function (a) {
        a && null != this.level.moves && this.movesFromString(this.level.moves);
        this.enable.undoredo && this.undoAll()
    };
    this.onRedoAll = function (a) {
        a ? (this.autoValueMarkers = !0, this.initValueMarkers(), this.updateValueMarkers()) : this.enable.undoredo && this.redoAll()
    };
    this.onSolve = function (a) {
        try {
            (a || this.enable.solve) && this.solve()
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onCheck = function (a) {
        try {
            a ? this.solve() : this.enable.check && (this.display.errors = !this.display.errors, this.check())
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onSolution = function (a) {
        try {
            this.enable.solution && this.showSolution()
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onSelect = function (a) {
        this.enable.prevnext && this.select(a)
    };
    this.onPrev = function (a) {
        if (this.enable.prevnext)if (a)this.onSelect(0); else this.onSelect(this.level.nr - 1)
    };
    this.onNext = function (a) {
        if (this.enable.prevnext)if (a)this.onSelect(this.levels.length - 1); else this.onSelect(this.level.nr + 1)
    };
    this.onFirst = function (a) {
        if (this.enable.prevnext)this.onSelect(0)
    };
    this.onLast = function (a) {
        if (this.enable.prevnext)this.onSelect(this.levels.length - 1)
    };
    this.onLevel = function (a) {
        try {
            if (this.enable.prevnext) {
                this.hidePopups();
                var b = this.getElementPosition(this.uie.level), c = this.uie.levellist, d = '<option value="0" style="color: red;">' + this.uis.get("cancel") + "</option>\n";
                for (a = 1; a <= this.levels.length; a++)d += '<option value="' + a + '">' + a + "</option>\n";
                c.innerHTML = d;
                c.style.zindex = 2;
                c.style.position = "absolute";
                c.style.left = b.left + "px";
                c.style.top = b.top + this.uie.save.height +
                "px";
                c.style.display = "inline";
                c.onchange = this.onLevel2
            }
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.onLevel2 = function () {
        try {
            var a = f.uie.levellist;
            a.style.display = "none";
            -1 != a.selectedIndex && 0 != a.selectedIndex && (f.onSelect.call(f, a.selectedIndex - 1), f.paint())
        } catch (b) {
            throw f.exception(b), b;
        }
    };
    this.onLoad = function (a) {
        this.onLoadSave(0, a)
    };
    this.onSave = function (a) {
        this.onLoadSave(1, a)
    };
    this.onLoadSave = function (a, b) {
        try {
            if (this.enable.loadsave)if (b)0 == a ? this.loadPuzzle(0) : this.savePuzzle(0); else {
                this.hidePopups();
                for (var c = this.getElementPosition(0 == a ? this.uie.load : this.uie.save), d = this.uie.savelist, e = '<option value="0" style="color: red;">' + this.uis.get("server") + "</option>\n", g = 1; 9 > g; g++)e += '<option value="' + g + '" style="color: ' + (this.savedGames[g] ? "blue" : "black") + ';">' + this.uis.get("local") + "</option>\n";
                e += '<option value="10" style="color: red;">' + this.uis.get("cancel") + "</option>\n";
                d.innerHTML = e;
                d.style.zindex = 2;
                d.style.position = "absolute";
                d.style.left = c.left + "px";
                d.style.top = c.top + this.uie.save.height +
                "px";
                d.style.display = "inline";
                d.ojfunction = 0 == a ? this.loadPuzzle : this.savePuzzle;
                d.onchange = this.onLoadSave2
            }
        } catch (f) {
            throw this.exception(f), f;
        }
    };
    this.onLoadSave2 = function () {
        try {
            var a = f.uie.savelist;
            a.style.display = "none";
            9 != a.selectedIndex && (this.ojfunction.call(f, a.selectedIndex), f.paint())
        } catch (b) {
            throw f.exception(b), b;
        }
    };
    this.onVMarkers = function (a) {
        try {
            this.enable.vmarkers && (a ? (this.autoValueMarkers = !0, this.initValueMarkers(), this.updateValueMarkers()) : this.toggleMarkerMode())
        } catch (b) {
            throw this.exception(b),
                b;
        }
    };
    this.onSMarkers = function (a) {
        try {
            this.showKeypad(2, null, null)
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onSMarkers2 = function (a, b) {
        try {
            99 == b ? this.removeAllMarkers() : 98 == b ? this.current.marker = nil : null == a ? this.current.marker = b : this.toggleMarker(a, b), this.paint()
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.onCMarkers = function (a) {
        try {
            this.showKeypad(1, null, null)
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onCMarkers2 = function (a, b) {
        try {
            10 == b ? this.acceptColor() : 11 == b ? this.rejectColor() : null != a ? this.makeMove(a,
                a.value, b) : (this.setColor(b), this.current.marker = nil)
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.onValues = function (a) {
        try {
            null != this.keypadValues && this.showKeypad(0, null, this.keypadValues)
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onValues2 = function (a, b) {
        try {
            this.current.value = b, this.current.type = this.item.cell, this.current.marker = nil, a && a.type == this.item.cell && this.makeMove(a, b)
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.onAction = function () {
        try {
            this.timer.activity()
        } catch (a) {
            this.exception(a)
        }
    };
    this.onTouchStart = function (a) {
        try {
            if (a = a || window.event, 1 != a.touches.length)this.pointer.dragging && this.dragEnd(), this.pointer.dragging = !1, this.pointer.item = nil, this.cancelEvent(a); else {
                this.pointer.x = a.touches[0].clientX;
                this.pointer.y = a.touches[0].clientY;
                this.pointer.magic++;
                this.pointer.cancel = !1;
                this.onCanvasDown(a, this.pointer.x, this.pointer.y, 1);
                var b = this, c = this.pointer.magic;
                setTimeout(function () {
                    b.onTouchPressed.call(b, c)
                }, this.uim.longTouch)
            }
        } catch (d) {
            this.exception(d)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onTouchPressed = function (a) {
        try {
            a == this.pointer.magic && (this.pointer.magic++, this.pointer.cancel = !0)
        } catch (b) {
            this.exception(b)
        }
    };
    this.onTouchMove = function (a) {
        try {
            if (a = a || window.event, !this.pointer.scrolling && !this.pointer.zooming && 1 == a.touches.length) {
                var b = this.current.item;
                this.onCanvasMove(a, this.pointer.x, this.pointer.y, 1);
                this.pointer.x = a.touches[0].clientX;
                this.pointer.y = a.touches[0].clientY;
                b != this.current.item && this.pointer.magic++
            } else {
                var c = a.touches[0].clientX - this.pointer.x, d = a.touches[0].clientY -
                    this.pointer.y;
                if (0 != c || 0 != d)this.onCanvasScroll(a, c, d, 0), this.pointer.x = a.touches[0].clientX, this.pointer.y = a.touches[0].clientY, this.pointer.magic++
            }
        } catch (e) {
            this.exception(e)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onTouchEnd = function (a) {
        try {
            a = a || window.event;
            if (!this.pointer.cancel)this.onCanvasUp(a, this.pointer.x, this.pointer.y, 1);
            this.pointer.distance = nil;
            this.pointer.magic++
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onMouseDown = function (a) {
        try {
            a = a || window.event, this.pointer.button =
                a.which && 3 == a.which || a.button && 2 == a.button ? 2 : 1, this.onCanvasDown(a, a.clientX, a.clientY, this.pointer.button), this.pointer.x = a.clientX, this.pointer.y = a.clientY
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onMouseUp = function (a) {
        try {
            a = a || window.event, this.pointer.button = a.which && 3 == a.which || a.button && 2 == a.button ? 2 : 1, this.onCanvasUp(a, a.clientX, a.clientY, this.pointer.button), this.pointer.x = a.clientX, this.pointer.y = a.clientY, this.pointer.button = 0
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onMouseMove = function (a) {
        try {
            a = a || window.event;
            if (a.ctrlKey && 1 == this.pointer.button)if (a.clientX > this.pointer.x)this.onCanvasZoom(a, 1, this.pointer.button); else this.onCanvasZoom(a, -1, this.pointer.button); else if (a.altKey && 1 == this.pointer.button)this.onCanvasScroll(a, a.clientX - this.pointer.x, a.clientY - this.pointer.y, 0); else this.onCanvasMove(a, a.clientX, a.clientY, this.pointer.button);
            this.pointer.x = a.clientX;
            this.pointer.y = a.clientY
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onMouseOut =
        function (a) {
            try {
                a = a || window.event, this.onCanvasOut(a, a.clientX, a.clientY, this.pointer.button), this.pointer.x = a.clientX, this.pointer.y = a.clientY, this.pointer.button = 0
            } catch (b) {
                this.exception(b)
            } finally {
                this.cancelEvent(a)
            }
        };
    this.onMouseWheel = function (a) {
        try {
            a = a || window.event
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onCanvasDown = function (a, b, c, d) {
        try {
            this.onAction();
            this.paintMessage("");
            var e = this.getItemFromXY(b, c);
            null != e && (this.moveTo(e), this.pointer.button = d, this.pointer.item =
                e, this.keypad.hide.call(this.keypad))
        } catch (f) {
            throw this.exception(f), f;
        }
    };
    this.onCanvasZoom = function (a, b, c) {
        try {
            this.onAction(), this.zoom.x = this.unit.x + b, this.zoom.y = this.unit.y + b, this.zoom.auto = !1, this.pointer.zooming = !0, this.paint()
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.onCanvasScroll = function (a, b, c, d) {
        try {
            this.onAction(), this.config.touchscreen ? (this.base.x += b, this.base.y += c, this.pointer.scrolling = !0, this.paint()) : (this.uie.scroller.scrollLeft += b * this.unit.x, this.uie.scroller.scrollTop +=
                c * this.unit.y)
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.onCanvasMove = function (a, b, c, d) {
        try {
            this.onAction();
            var e = this.getItemFromXY(b, c);
            if (!(null == e || e == this.current.item)) {
                var f = 0 != this.labels.north || 0 != this.labels.south || 0 != this.labels.east || 0 != this.labels.west;
                this.enable.dragging && 0 != this.pointer.button ? (1 == d ? this.dragTo(e, this.current.item, a.shiftKey) : this.dragTo(e, this.current.item, !0), f = !0) : this.moveTo(e);
                var h = this.display.cursor;
                this.display.cursor = !1;
                f || h ? this.paint() : this.paintCursor()
            }
        } catch (k) {
            throw this.exception(k),
                k;
        }
    };
    this.onCanvasUp = function (a, b, c, d) {
        try {
            if (this.onAction(), this.pointer.zooming || this.pointer.scrolling)this.pointer.zooming = this.pointer.scrolling = !1; else {
                var e = this.getItemFromXY(b, c), f = this.pointer.item;
                this.pointer.item = null;
                this.pointer.button = 0;
                if (this.pointer.dragging)this.dragEnd(), this.pointer.dragging = !1, this.paint(); else if (this.moveTo(e), !(null == e || null == this.current.item) && f == this.current.item)1 != d && this.enable.cells ? null != this.keypadValues && !this.enable.keypad ? this.showKeypad(0, this.current.item,
                    this.keypadValues) : this.enable.smarkers ? this.showKeypad(2, this.current.item, null) : this.makeMove(null, null, null, !0) : 1 == d && (a.ctrlKey ? this.makeMove(this.current.item, this.current.item.value) : this.enable.keypad && this.current.marker == nil && this.enable.cells && this.current.item.type == this.item.cell ? this.keypadValues && this.showKeypad(0, this.current.item, this.keypadValues) : this.makeMove(null, null, null, !1)), this.paint()
            }
        } catch (h) {
            throw this.exception(h), h;
        }
    };
    this.onCanvasOut = function (a) {
        try {
            this.onAction(),
            this.pointer.dragging && this.dragEnd(), this.pointer.dragging = !1, this.pointer.item = nil, this.moveTo(null), this.paint()
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.onContextMenu = function (a) {
        this.cancelEvent(a);
        return !1
    };
    this.onButtonOver = function (a) {
        try {
            f.onAction(), f.config.touchscreen || (a = a || window.event, this.style.padding = f.uim.buttonPadding + "px", this.style.borderStyle = "solid", this.style.borderWidth = f.uim.buttonBorder + "px", this.style.borderTopColor = f.uic.buttonBorderLight, this.style.borderLeftColor =
                f.uic.buttonBorderLight, this.style.borderRightColor = f.uic.buttonBorderDark, this.style.borderBottomColor = f.uic.buttonBorderDark)
        } catch (b) {
            f.exception(b)
        } finally {
            f.cancelEvent(a)
        }
    };
    this.onButtonOut = function (a) {
        try {
            f.onAction(), f.config.touchscreen || (a = a || window.event, this.style.borderWidth = "0px", this.style.padding = f.uim.buttonPadding + f.uim.buttonBorder + "px")
        } catch (b) {
            f.exception(b)
        } finally {
            f.cancelEvent(a)
        }
    };
    this.onButtonDown = function (a) {
        try {
            f.onAction(), f.paintMessage(""), a = a || window.event, f.cancelEvent(a),
                this.ojtime = a.timeStamp, f.config.touchscreen || (this.style.padding = f.uim.buttonPadding + "px", this.style.borderWidth = f.uim.buttonBorder + "px", this.style.borderStyle = "solid", this.style.borderTopColor = f.uic.buttonBorderDark, this.style.borderLeftColor = f.uic.buttonBorderDark, this.style.borderRightColor = f.uic.buttonBorderLight, this.style.borderBottomColor = f.uic.buttonBorderLight)
        } catch (b) {
            f.exception(b)
        } finally {
            f.cancelEvent(a)
        }
    };
    this.onButtonUp = function (a) {
        try {
            a = a || window.event, this.ojfunction.call(f, a.altKey ||
            a.ctrlKey || 2 == a.button || a.timeStamp - this.ojtime > f.uim.longTouch, a), f.onButtonOver.call(this, a), f.paint()
        } catch (b) {
            f.exception(b)
        } finally {
            f.cancelEvent()
        }
    };
    this.onKeyDown = function (a) {
        try {
            this.onAction();
            this.paintMessage("");
            a = a || window.event;
            var b = a.keyCode;
            if (!(16 <= b && 18 >= b) && (a.ctrlKey || a.altKey || a.shiftKey || !(65 <= b && 90 >= b || 48 <= b && 57 >= b))) {
                var c = !1;
                if (a.shiftKey && a.ctrlKey)switch (c = !0, b) {
                    case 38:
                        this.dragToDxDy(0, -1, !0);
                        break;
                    case 40:
                        this.dragToDxDy(0, 1, !0);
                        break;
                    case 37:
                        this.dragToDxDy(-1, 0, !0);
                        break;
                    case 39:
                        this.dragToDxDy(1, 0, !0);
                        break;
                    default:
                        c = !1
                }
                if (a.altKey && !c) {
                    c = !0;
                    switch (b) {
                        case 38:
                            this.onCanvasScroll(null, 0, -10, 0);
                            break;
                        case 40:
                            this.onCanvasScroll(null, 0, 10, 0);
                            break;
                        case 37:
                            this.onCanvasScroll(null, -10, 0, 0);
                            break;
                        case 39:
                            this.onCanvasScroll(null, 10, 0, 0);
                            break;
                        case 112:
                            this.onSaveImage("c");
                            break;
                        case 113:
                            this.onSaveImage("d");
                            break;
                        case 114:
                            this.onSaveImage("e");
                            break;
                        case 115:
                            c = !1;
                            return;
                        case 123:
                            ojassert(!1, "Alt+F12");
                            break;
                        default:
                            c = !1
                    }
                    this.enable.colors && (48 <= b && 57 >= b) && (this.onCMarkers2(null,
                        b - 48), c = !0)
                }
                if (a.ctrlKey && !c) {
                    c = !0;
                    switch (b) {
                        case 38:
                            this.onCanvasZoom(null, -10);
                            break;
                        case 40:
                            this.onCanvasZoom(null, 10);
                            break;
                        case 37:
                            this.onCanvasZoom(null, -1);
                            break;
                        case 39:
                            this.onCanvasZoom(null, 1);
                            break;
                        case 34:
                            this.onNext();
                            break;
                        case 33:
                            this.onPrev();
                            break;
                        case 36:
                            this.onFirst();
                            break;
                        case 35:
                            this.onLast();
                            break;
                        case 112:
                            this.onSaveImage("cd");
                            break;
                        case 83:
                            this.onSave();
                            break;
                        case 76:
                            this.onLoad();
                            break;
                        case 89:
                            this.onRedoOne();
                            break;
                        case 90:
                            this.onUndoOne();
                            break;
                        case 77:
                            this.removeAllMarkers();
                            break;
                        default:
                            c = !1
                    }
                    if (!c && this.enable.colors && null != this.current.item)if (c = !0, 48 <= b && 57 >= b)this.onCMarkers2(this.current.item, b - 48); else 13 == b || 32 == b ? this.makeMove(this.current.item, this.current.item.value) : c = !1;
                    if (!c && this.enable.smarkers && null != this.current.item) {
                        var d = this.current.item, c = !0;
                        switch (b) {
                            case 81:
                                this.toggleMarker(d, this.marker.circle);
                                break;
                            case 87:
                                this.toggleMarker(d, this.marker.square);
                                break;
                            case 69:
                                this.toggleMarker(d, this.marker.dot);
                                break;
                            case 82:
                                this.toggleMarker(d, this.marker.decagon);
                                break;
                            case 84:
                                this.toggleMarker(d, this.marker.cross);
                                break;
                            case 88:
                                this.toggleMarker(d, this.marker.cross);
                                break;
                            case 65:
                                this.toggleMarker(d, this.marker.letterA);
                                break;
                            case 66:
                                this.toggleMarker(d, this.marker.letterB);
                                break;
                            case 67:
                                this.toggleMarker(d, this.marker.letterC);
                                break;
                            case 68:
                                this.toggleMarker(d, this.marker.letterD);
                                break;
                            default:
                                c = !1
                        }
                    }
                }
                if (a.shiftKey && !c)switch (c = !0, b) {
                    case 38:
                        this.dragToDxDy(0, -1, !1);
                        break;
                    case 40:
                        this.dragToDxDy(0, 1, !1);
                        break;
                    case 37:
                        this.dragToDxDy(-1, 0, !1);
                        break;
                    case 39:
                        this.dragToDxDy(1,
                            0, !1);
                        break;
                    case 115:
                        this.showSolution();
                        break;
                    case 117:
                        this.onSolve(!0);
                        break;
                    case 118:
                        this.initValueMarkers();
                        break;
                    case 119:
                        this.updateValueMarkers();
                        break;
                    case 120:
                        this.onShiftF9();
                        break;
                    case 121:
                        this.onShiftF10();
                        break;
                    case 122:
                        this.onDisplayScores();
                        break;
                    case 123:
                        this.onInfo(!0);
                        break;
                    default:
                        c = !1
                }
                if (!c)for (d = 0; d < this.codeToValue.length; d += 2)b == this.codeToValue[d] && (this.makeMove(null, this.codeToValue[d + 1]), c = !0);
                if (!c)switch (c = !0, b) {
                    case 45:
                        this.makeMove(null, null, null, !1);
                        break;
                    case 13:
                        this.makeMove(null,
                            null, null, !1);
                        break;
                    case 32:
                        this.makeMove(null, null, null, !0);
                        break;
                    case 27:
                        this.hidePopups();
                        break;
                    case 38:
                        this.moveToDxDy(0, -1);
                        break;
                    case 40:
                        this.moveToDxDy(0, 1);
                        break;
                    case 37:
                        this.moveToDxDy(-1, 0);
                        break;
                    case 39:
                        this.moveToDxDy(1, 0);
                        break;
                    case 33:
                        this.onUndoOne();
                        break;
                    case 34:
                        this.onRedoOne();
                        break;
                    case 36:
                        this.onUndoAll();
                        break;
                    case 35:
                        this.onRedoAll();
                        break;
                    case 112:
                        this.onInfo();
                        break;
                    case 113:
                        this.onMake();
                        break;
                    case 114:
                        this.onHint();
                        break;
                    case 115:
                        this.onSolution();
                        break;
                    case 116:
                        this.onReset();
                        break;
                    case 117:
                        this.onCheck();
                        break;
                    case 118:
                        this.onVMarkers();
                        break;
                    case 119:
                        this.acceptColor();
                        break;
                    case 120:
                        this.rejectColor();
                        break;
                    case 121:
                        this.onOptions();
                        break;
                    default:
                        c = !1;
                        break
                }
            }
        } catch (e) {
            this.exception(e)
        } finally {
            c && this.cancelEvent(a), c && this.paint()
        }
    };
    var y = null, z = 0;
    this.onKeyPress = function (a) {
        try {
            this.onAction();
            a = a || window.event;
            var b = 0 != a.which && 0 != a.charCode ? String.fromCharCode(a.which) : -1;
            if (!(a.altKey || -1 == b))if (this.cancelEvent(a), !a.ctrlKey) {
                var c = !1;
                if (this.current.item && this.current.item.type ==
                    this.item.cell && null != this.charToValue)for (var d = 0; d < this.charToValue.length; d += 2)if (b == this.charToValue[d]) {
                    var e = this.charToValue[d + 1];
                    if (this.editValueMarkers)for (var f = 0; f < this.valueToMarker.length; f += 2)e == this.valueToMarker[f] && this.toggleValueMarker(null, this.valueToMarker[f + 1]); else this.makeMove(null, e);
                    c = !0
                }
                !c && ("0" <= b && "9" >= b && this.cell.max >= this.cell.min && this.current.item && this.current.item.type == this.item.cell) && (d = b.charCodeAt(0) - 48, 9 < this.cell.max && (z + this.uim.multikey > a.timeStamp &&
                y == this.current.item) && (d = 10 * this.current.item.value + d), d >= this.cell.min && d <= this.cell.max && (this.editValueMarkers ? this.toggleValueMarker(null, this.marker.numberBase + d) : this.makeMove(null, d)), y = this.current.item, z = a.timeStamp, c = !0);
                !c && (this.enable.colors && "0" <= b && "9" >= b) && (this.onCMarkers2(null, b - 0), c = !0);
                if (!c && this.enable.smarkers && null != this.current.item && this.current.item.type == this.item.cell) {
                    var h = this.current.item, c = !0;
                    switch (b) {
                        case "q":
                            this.toggleMarker(h, this.marker.circle);
                            break;
                        case "w":
                            this.toggleMarker(h,
                                this.marker.square);
                            break;
                        case "e":
                            this.toggleMarker(h, this.marker.dot);
                            break;
                        case "r":
                            this.toggleMarker(h, this.marker.decagon);
                            break;
                        case "t":
                            this.toggleMarker(h, this.marker.cross);
                            break;
                        case "x":
                            this.toggleMarker(h, this.marker.cross);
                            break;
                        case "a":
                            this.toggleMarker(h, this.marker.letterA);
                            break;
                        case "b":
                            this.toggleMarker(h, this.marker.letterB);
                            break;
                        case "c":
                            this.toggleMarker(h, this.marker.letterC);
                            break;
                        case "d":
                            this.toggleMarker(h, this.marker.letterD);
                            break;
                        default:
                            c = !1;
                            break
                    }
                }
            }
        } catch (k) {
            this.exception(k)
        } finally {
            c &&
            this.cancelEvent(a), c && this.paint()
        }
    };
    this.onKeyUp = function (a) {
        try {
            a = a || window.event, 16 == a.keyCode && this.pointer.dragging && (this.dragEnd(), this.pointer.dragging = !1)
        } catch (b) {
            this.exception(b)
        } finally {
            this.cancelEvent(a)
        }
    };
    this.onDeviceOrientation = function (a) {
        try {
            if (this.tilt.active) {
                this.paintMessage("Orientation: " + (Math.round(100 * a.alpha) / 100).toString() + " \u2022 " + (Math.round(100 * a.beta) / 100).toString() + " \u2022 " + (Math.round(100 * a.gamma) / 100).toString() + " \u2022\u2022\u2022 " + this.tilt.beta.toString() +
                " \u2022 " + this.tilt.gamma.toString());
                var b = 0, c = 0;
                this.tilt.gamma && a.gamma > this.tilt.action && (b = 1);
                this.tilt.gamma && a.gamma < -this.tilt.action && (b = -1);
                this.tilt.beta && a.beta > this.tilt.action && (c = 1);
                this.tilt.beta && a.beta < -this.tilt.action && (c = -1);
                a.gamma > -this.tilt.reset && a.gamma < this.tilt.reset && (this.tilt.gamma = !0);
                a.beta > -this.tilt.reset && a.beta < this.tilt.reset && (this.tilt.beta = !0);
                if (0 != b || 0 != c)this.moveToDxDy(b, c), this.paint(), this.tilt.beta = this.tilt.gamma = !1
            }
        } catch (d) {
            this.exception(d)
        }
    };
    this.onBeforeUnload =
        function (a) {
            try {
                ojdebug("onBeforeUnload")
            } catch (b) {
                this.exception(b)
            } finally {
                this.cancelEvent(a)
            }
        };
    this.hidePopups = function () {
        try {
            this.keypad && this.keypad.hide(), this.uie.zoomlist && (this.uie.zoomlist.style.display = "none"), this.uie.savelist && (this.uie.savelist.style.display = "none"), this.uie.levellist && (this.uie.levellist.style.display = "none")
        } catch (a) {
            throw this.exception(a), a;
        }
    };
    this.cancelEvent = function (a) {
        try {
            a && (a.preventDefault(), a.returnValue = !1, window.event && (window.event.returnValue = !1), a.stopPropagation())
        } catch (b) {
            f.exception(b)
        }
    };
    this.getElementPosition = function (a) {
        try {
            var b = a.getBoundingClientRect(), c = document.body, d = document.documentElement, e = b.left + (window.pageXOffset || d.scrollLeft || c.scrollLeft) - (d.clientLeft || c.clientLeft || 0);
            return {
                top: Math.round(b.top + (window.pageYOffset || d.scrollTop || c.scrollTop) - (d.clientTop || c.clientTop || 0)),
                left: Math.round(e)
            }
        } catch (f) {
            throw this.exception(f), f;
        }
    };
    this.getItemFromXY = function (a, b) {
        try {
            var c = this.canvas.getBoundingClientRect();
            a -= c.left;
            b -= c.top;
            c = null;
            if (this.enable.lines) {
                var d =
                    this.enable.cells ? Math.max(this.unit.x / 5, 5) : this.unit.x / 3, e = Math.min(this.unit.x / 6, 5), f = Math.floor((a - this.base.x) / this.unit.x), h = Math.floor((b - this.base.y + this.unit.y / 2) / this.unit.y);
                if (0 <= f && f < this.size.x && 0 <= h && h <= this.size.y) {
                    var k = f * this.unit.x + this.base.x, m = h * this.unit.y + this.base.y, n = this.canvas.getContext("2d");
                    n.save();
                    n.beginPath();
                    n.moveTo(k + e, m);
                    n.lineTo(k + d, m - d);
                    n.lineTo(k + this.unit.x - d, m - d);
                    n.lineTo(k + this.unit.x - e, m);
                    n.lineTo(k + this.unit.x - d, m + d);
                    n.lineTo(k + d, m + d);
                    n.closePath();
                    n.isPointInPath(a,
                        b) && (c = this.board.h[f][h]);
                    n.restore()
                }
                f = Math.floor((a - this.base.x + this.unit.x / 2) / this.unit.x);
                h = Math.floor((b - this.base.y) / this.unit.y);
                0 <= f && (f <= this.size.x && 0 <= h && h < this.size.y) && (k = f * this.unit.x + this.base.x, m = h * this.unit.y + this.base.y, n = this.canvas.getContext("2d"), n.save(), n.beginPath(), n.moveTo(k, m + e), n.lineTo(k - d, m + d), n.lineTo(k - d, m + this.unit.y - d), n.lineTo(k, m + this.unit.y - e), n.lineTo(k + d, m + this.unit.y - d), n.lineTo(k + d, m + d), n.closePath(), n.isPointInPath(a, b) && (c = this.board.v[f][h]), n.restore())
            }
            if (this.enable.cells &&
                null == c && (f = Math.floor((a - this.base.x) / this.unit.x), h = Math.floor((b - this.base.y) / this.unit.y), 0 <= f && f < this.size.x && 0 <= h && h < this.size.y)) {
                var l = 4 * this.unit.x / 10, p = 4 * this.unit.y / 10, k = f * this.unit.x + this.base.x, m = h * this.unit.y + this.base.y, n = this.canvas.getContext("2d");
                n.save();
                n.beginPath();
                n.moveTo(k + l, m);
                n.lineTo(k + this.unit.x - l, m);
                n.lineTo(k + this.unit.x, m + p);
                n.lineTo(k + this.unit.x, m + this.unit.y - p);
                n.lineTo(k + this.unit.x - l, m + this.unit.y);
                n.lineTo(k + l, m + this.unit.y);
                n.lineTo(k, m + this.unit.y - p);
                n.lineTo(k,
                    m + p);
                n.closePath();
                n.isPointInPath(a, b) && (c = this.board.c[f][h]);
                n.restore()
            }
            return c
        } catch (q) {
            throw this.exception(q), q;
        }
    };
    this.showKeypad = function (a, b, c) {
        try {
            this.keypad.show(a, b, c)
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paint = function () {
        try {
            if (this.paintMessage(), this.paintInfo(), this.paintInit(), (this.enable.pgrid || this.paintToImage) && this.paintFrame(), this.enable.pcells && this.paintCells(), this.enable.pgrid ? this.paintGrid() : this.enable.plines && this.paintLines(), this.paintCursor(), this.enable.pnodes &&
                this.paintNodes(), this.paintDone(), this.enable.current && this.paintCurrentValue(), this.enable.smarkers && this.paintCurrentMarker(), this.paintCurrentLevel(), this.uie.scroller.style.background = this.solved ? this.result.code == this.result.won ? this.uic.won : this.result.code == this.result.lost ? this.uic.lost : this.result.code == this.result.draw ? this.uic.draw : this.uic.solved : this.uic.canvas, this.uie.cmarker.style.background = 0 == this.current.color ? this.uic.toolbarPanel : this.uic.light[this.current.color], this.uie.vmarker.style.background =
                    this.editValueMarkers ? this.uic.buttonHighlight : this.uic.toolbarPanel, this.uie.tilt.style.background = this.tilt.active ? this.uic.buttonHighlight : this.uic.toolbarPanel, this.paintToImage && this.infoText && this.moves.current == nil) {
                var a = this.canvas.getContext("2d");
                a.fillStyle = this.uic.white;
                a.fillRect(0, 0, this.canvas.width, this.uim.infoHeight);
                a.textAlign = "center";
                a.textBaseline = "middle";
                a.font = Math.floor(60 * this.uim.infoHeight / 100).toString() + "px sans-serif";
                a.fillStyle = this.uic.black;
                a.fillText(this.infoText,
                    this.canvas.width / 2, this.uim.infoHeight / 2)
            }
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.paintInfo = function (a) {
        try {
            a && (this.infoText = a), this.infoText ? (this.uie.info.style.display = "", this.uie.info.innerHTML = this.infoText) : this.uie.info.style.display = "none"
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.paintMessage = function (a) {
        try {
            var b = "&nbsp;";
            void 0 !== a && null != a && (this.messageText = a);
            this.messageText ? b = this.messageText : this.solved ? b = this.result.code == this.result.won ? this.uis.get("won") : this.result.code ==
            this.result.lost ? this.uis.get("lost") : this.result.code == this.result.draw ? this.uis.get("draw") : this.uis.get("solved") : this.level.author ? b = this.uis.get("author") + ": " + this.level.author : this.level.title && (b = this.uis.get("title") + ": " + this.level.title);
            this.uie.message.innerHTML = b
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintCurrentLevel = function () {
        try {
            if (!(2 > this.levels.length)) {
                var a = this.uie.level, b = a.getContext("2d");
                b.fillStyle = this.uic.toolbarPanel;
                b.fillRect(0, 0, a.width, a.height);
                b.fillStyle =
                    this.uic.black;
                this.paintCaption((this.level.nr + 1).toString(), b, {x: 0, y: 0, w: a.width, h: a.height, scale: 100})
            }
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintCurrentValue = function () {
        var a = this.uie.value, b = a.getContext("2d");
        b.fillStyle = this.uic.white;
        b.fillRect(0, 0, a.width, a.height)
    };
    this.paintCurrentMarker = function () {
        try {
            var a = this.uie.smarker, b = a.getContext("2d");
            b.fillStyle = this.uic.white;
            b.fillRect(0, 0, a.width, a.height);
            var c = {
                x: 0, y: 0, w: a.width, h: a.height, scale: 80, fill: this.uic.none, stroke: this.uic.black,
                color: this.uic.black
            };
            switch (this.current.marker) {
                case this.marker.cross:
                    this.paintCross(b, c);
                    break;
                case this.marker.circle:
                    this.paintCircle(b, c);
                    break;
                case this.marker.square:
                    this.paintSquare(b, c);
                    break;
                case this.marker.decagon:
                    this.paintDecagon(b, c);
                    break;
                case this.marker.dot:
                    this.paintDot(b, c);
                    break;
                case this.marker.letterA:
                    this.paintCaption("a", b, c);
                    break;
                case this.marker.letterB:
                    this.paintCaption("b", b, c);
                    break;
                case this.marker.letterC:
                    this.paintCaption("c", b, c);
                    break;
                case this.marker.letterD:
                    this.paintCaption("d",
                        b, c);
                    break;
                default:
                    c.stroke = "#339933", this.paintCircle(b, c), c.color = "#ff3333", this.paintDot(b, c)
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintInit = function () {
        try {
            var a = this.canvas.getContext("2d"), b = document.body.getBoundingClientRect(), c = b.width - 2 * this.uim.padding - 2 * this.uim.margin, d = window.innerHeight - this.uie.toolbar.getBoundingClientRect().height - this.uie.info.getBoundingClientRect().height - this.uie.message.getBoundingClientRect().height - 2 * this.uim.margin - 2 * this.uim.padding, e = Math.floor(c),
                f = Math.floor(d);
            this.zoom.auto || 0 == this.zoom.x || 0 == this.zoom.y ? (this.unit.x = Math.floor((e - 2 * this.uim.margin - 2 * this.uim.padding) / this.size.x), this.unit.y = Math.floor((f - 2 * this.uim.margin - 2 * this.uim.padding) / this.size.y)) : (this.unit.x = this.zoom.x, this.unit.y = this.zoom.y);
            this.unit.x = this.unit.y = Math.min(this.unit.x, this.unit.y, this.unit.max);
            this.unit.x = this.unit.y = Math.max(this.unit.x, this.unit.min);
            var h = this.unit.x * this.size.x + 2 * this.uim.padding + 1, k = this.unit.y * this.size.y + 2 * this.uim.padding + 1;
            this.config.touchscreen &&
            (h = Math.min(h, e), k = Math.min(k, f));
            if (!this.config.touchscreen || 0 == this.base.x && 0 == this.base.y)this.base.x = this.base.y = this.uim.padding;
            this.paintToImage && (this.infoText && this.moves.current == nil) && (k += this.uim.infoHeight, this.base.y += this.uim.infoHeight);
            a.canvas.width = h;
            a.canvas.height = k;
            var m = 2 * this.uim.margin, l = this.uie.scroller, k = h = 0;
            a.canvas.width > e && (h = b.right - b.left);
            k = a.canvas.height > f ? f : a.canvas.height + m + 5;
            l.style.width = 0 == h ? "" : l.style.width = h.toString() + "px";
            l.style.height = 0 == k ? "" : l.style.height =
                k.toString() + "px";
            this.config.touchscreen && (this.base.x > this.uim.padding && (this.base.x = this.uim.padding), this.base.y > this.uim.padding && (this.base.y = this.uim.padding), c = a.canvas.width - this.base.x - this.unit.x * this.size.x - this.uim.padding, d = a.canvas.height - this.base.y - this.unit.y * this.size.y - this.uim.padding, 0 < c && (this.base.x += c), 0 < d && (this.base.y += d))
        } catch (p) {
            throw this.exception(p), p;
        }
    };
    this.paintDone = function () {
    };
    this.paintFrame = function () {
        try {
            var a = this.canvas.getContext("2d");
            a.fillStyle = this.uic.canvas;
            a.fillRect(0, 0, a.canvas.width, a.canvas.height);
            a.fillStyle = this.uic.light[0];
            a.fillRect(this.base.x, this.base.y, this.size.x * this.unit.x, this.size.y * this.unit.y)
        } catch (b) {
            throw this.exception(b), b;
        }
    };
    this.paintGrid = function () {
        try {
            var a = this.canvas.getContext("2d"), b = this.base.x + this.labels.west * this.unit.x + 0.5, c = this.base.y + this.labels.north * this.unit.y + 0.5, d = this.base.x + (this.size.x - this.labels.east) * this.unit.x + 0.5, e = this.base.y + (this.size.y - this.labels.south) * this.unit.y + 0.5;
            if (this.enable.pgridlines &&
                0 != this.uim.grid) {
                a.strokeStyle = this.uic.grid;
                a.lineWidth = this.uim.grid;
                a.beginPath();
                for (var f = 0, h = this.size.x - this.labels.west - this.labels.east; f < h; f++) {
                    var k = b + (f + 1) * this.unit.x;
                    a.moveTo(k, c);
                    a.lineTo(k, e)
                }
                for (var f = 0, m = this.size.y - this.labels.north - this.labels.south; f < m; f++) {
                    var l = c + (f + 1) * this.unit.y;
                    a.moveTo(b, l);
                    a.lineTo(d, l)
                }
                a.stroke()
            }
            this.enable.pedgelines && 0 != this.uim.edge && (a.lineWidth = this.uim.edge, a.strokeStyle = this.uic.edge, a.beginPath(), a.moveTo(b, c), a.lineTo(b, e), a.moveTo(d, c), a.lineTo(d,
                e), a.moveTo(b, c), a.lineTo(d, c), a.moveTo(b, e), a.lineTo(d, e), a.stroke())
        } catch (p) {
            throw this.exception(p), p;
        }
    };
    this.paintCells = function () {
        try {
            for (var a = 0; a < this.size.x; a++)for (var b = 0; b < this.size.y; b++) {
                var c = this.board.c[a][b];
                c.areas != this.area.outside && (c.px = this.base.x + c.x * this.unit.x, c.py = this.base.y + c.y * this.unit.y, this.paintCell(c))
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintCell = function (a) {
    };
    this.paintLines = function () {
        try {
            if (!(0 == this.uim.wall && 0 == this.uim.grid)) {
                for (var a = 0; a < this.board.l.length; a++) {
                    var b =
                        this.board.l[a];
                    b.px = this.base.x + b.x * this.unit.x;
                    b.py = this.base.y + b.y * this.unit.y;
                    b.value != this.line.wall && this.paintLine(b)
                }
                for (a = 0; a < this.board.l.length; a++)b = this.board.l[a], b.px = this.base.x + b.x * this.unit.x, b.py = this.base.y + b.y * this.unit.y, b.value == this.line.wall && this.paintLine(b)
            }
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintLine = function (a) {
        try {
            var b = this.canvas.getContext("2d"), c = 0;
            if (a.value == this.line.wall)c = this.uim.wall, b.strokeStyle = 0 == a.color ? this.uic.wall : this.uic.dark[a.color]; else if (a.value ==
                this.line.grid)c = this.uim.grid, b.strokeStyle = 0 == a.color ? this.uic.grid : this.uic.light[a.color]; else {
                if (a.value == this.line.cross) {
                    b.strokeStyle = this.uic.dark[a.color];
                    b.lineWidth = 2;
                    a.type == this.item.hline ? this.paintHCross(a) : this.paintVCross(a);
                    return
                }
                if (a.value == this.line.none)return;
                throw"paintLine: Illegal value";
            }
            0 != c && (b.lineWidth = c, !this.solved && this.display.errors && (0 != a.count ? b.strokeStyle = this.uic.dark[a.count % 10] : a.error && (b.strokeStyle = this.uic.error)), a.type == this.item.hline ? this.paintHLine(a) :
                this.paintVLine(a))
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintHLine = function (a) {
        try {
            var b = this.canvas.getContext("2d"), c = a.px + 0.5, d = a.py + 0.5;
            b.lineCap = "round";
            b.beginPath();
            b.moveTo(c, d);
            b.lineTo(c + this.unit.x, d);
            b.stroke()
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.paintVLine = function (a) {
        try {
            var b = this.canvas.getContext("2d"), c = a.px + 0.5, d = a.py + 0.5;
            b.lineCap = "round";
            b.beginPath();
            b.moveTo(c, d);
            b.lineTo(c, d + this.unit.y);
            b.stroke()
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.paintHCross = function (a) {
        try {
            var b =
                this.canvas.getContext("2d"), c = a.px + this.unit.x / 2 + 0.5, d = a.py + 0.5;
            b.lineCap = "round";
            b.beginPath();
            b.moveTo(c - 3, d - 3);
            b.lineTo(c + 3, d + 3);
            b.moveTo(c + 3, d - 3);
            b.lineTo(c - 3, d + 3);
            b.stroke()
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.paintVCross = function (a) {
        try {
            var b = this.canvas.getContext("2d"), c = a.px + 0.5, d = a.py + this.unit.x / 2 + 0.5;
            b.lineCap = "round";
            b.beginPath();
            b.moveTo(c - 3, d - 3);
            b.lineTo(c + 3, d + 3);
            b.moveTo(c + 3, d - 3);
            b.lineTo(c - 3, d + 3);
            b.stroke()
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.paintNodes = function () {
        try {
            for (var a =
                0; a <= this.size.x; a++)for (var b = 0; b <= this.size.y; b++) {
                var c = this.board.n[a][b];
                c.px = this.base.x + c.x * this.unit.x;
                c.py = this.base.y + c.y * this.unit.y;
                this.paintNode(c)
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintNode = function (a) {
    };
    this.paintCursor = function (a, b) {
        try {
            if (this.enable.pcursor)if (a) {
                var c = this.canvas.getContext("2d");
                c.beginPath();
                c.lineWidth = b;
                c.strokeStyle = this.uic.cursor;
                c.lineCap = "round";
                c.rect(a.px + 2, a.py + 2, this.unit.x - 3, this.unit.y - 3);
                c.stroke()
            } else if (!(null == this.current.item ||
                this.current.item.type != this.item.cell || this.current.item.areas <= this.area.outside))if (this.display.cursor && this.paintCursor(this.current.item, this.uim.cellCursor), !this.paintToImage) {
                for (c = 0; c < this.labels.west; c++)a = this.board.c[c][this.current.item.y], a.areas == this.area.label && this.paintCursor(a, this.uim.labelCursor);
                for (var d = 0; d < this.labels.north; d++)a = this.board.c[this.current.item.x][d], a.areas == this.area.label && this.paintCursor(a, this.uim.labelCursor);
                for (c = this.size.x - this.labels.east; c < this.size.x; c++)a =
                    this.board.c[c][this.current.item.y], a.areas == this.area.label && this.paintCursor(a, this.uim.labelCursor);
                for (d = this.size.y - this.labels.south; d < this.size.y; d++)a = this.board.c[this.current.item.x][d], a.areas == this.area.label && this.paintCursor(a, this.uim.labelCursor)
            }
        } catch (e) {
            throw this.exception(e), e;
        }
    };
    this.paintSymbolMarkers = function (a) {
        try {
            if (0 != a.markers.length()) {
                var b = {stroke: this.uic.smarkers, color: this.uic.smarkers, fill: this.uic.none};
                a.markers.get(this.marker.circle) && this.paintCircle(a, b);
                a.markers.get(this.marker.square) && this.paintSquare(a, b);
                a.markers.get(this.marker.decagon) && this.paintDecagon(a, b);
                a.markers.get(this.marker.cross) && this.paintCross(a, b);
                a.markers.get(this.marker.dot) && this.paintDot(a, b);
                if (a.value == nil && a.label == nil) {
                    var c = "";
                    a.markers.get(this.marker.letterA) && (c += "a");
                    a.markers.get(this.marker.letterB) && (c += "b");
                    a.markers.get(this.marker.letterC) && (c += "c");
                    a.markers.get(this.marker.letterD) && (c += "d");
                    0 != c.length && (b.scale = 50, this.paintCaption(c, a, b))
                }
            }
        } catch (d) {
            throw this.exception(d),
                d;
        }
    };
    this.paintValueMarkers = function (a) {
        try {
            if (this.enable.vmarkers && !(a.fixed || a.value != nil) && 0 != a.markers.length()) {
                var b = this.canvas.getContext("2d");
                b.fillStyle = this.uic.vmarkers;
                b.font = Math.floor(this.unit.y / 3).toString() + "px sans-serif";
                b.textAlign = "right";
                b.textBaseline = "top";
                for (var c = 2, d = "", e = 9; 0 <= e; e--)if (a.markers.get(this.marker.numberBase + e)) {
                    var f = e.toString(), h = b.measureText(f + d);
                    h.width < 80 * this.unit.x / 100 ? d = f + d : (b.fillText(d, a.px + 90 * this.unit.x / 100, a.py + this.unit.y / 3 * c + 1), c--, d = f)
                }
                for (e =
                         26; 0 <= e; e--)a.markers.get(this.marker.letterBase + e) && (f = String.fromCharCode(e + 65), h = b.measureText(f + d), h.width < 80 * this.unit.x / 100 ? d = f + d : (b.fillText(d, a.px + 90 * this.unit.x / 100, a.py + this.unit.y / 3 * c + 1), c--, d = f));
                "" != d && b.fillText(d, a.px + 90 * this.unit.x / 100, a.py + this.unit.y / 3 * c + 1)
            }
        } catch (k) {
            throw this.exception(k), k;
        }
    };
    this.paintDiagonal = function (a, b) {
        try {
            var c = a.px + this.uim.grid, d = a.py + this.uim.grid, e = this.unit.x - this.uim.grid, f = this.unit.y - this.uim.grid, h = this.canvas.getContext("2d");
            h.strokeStyle = this.uic.grid;
            h.lineWidth = this.uim.grid;
            h.setLineDash && (h.lineWidth = 2, h.setLineDash([2]));
            h.beginPath();
            1 == b ? (h.moveTo(c, d), h.lineTo(c + e, d + f)) : (h.moveTo(c + e, d), h.lineTo(c, d + f));
            h.stroke();
            h.setLineDash && h.setLineDash([])
        } catch (k) {
            throw this.exception(k), k;
        }
    };
    this.defaultParams = function (a, b) {
        try {
            if (!a)return null;
            var c = b ? ojclone(b) : {};
            a.px ? (void 0 === c.x && (c.x = a.px), void 0 === c.y && (c.y = a.py), void 0 === c.w && (c.w = this.unit.x), void 0 === c.h && (c.h = this.unit.y)) : (void 0 === c.x && (c.x = 0), void 0 === c.y && (c.y = 0), void 0 === c.w &&
            (c.w = 16), void 0 === c.h && (c.h = 16));
            return c
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintCaption = function (a, b, c) {
        try {
            if (c = this.defaultParams(b, c)) {
                c.scale || (c.scale = 66);
                c.text || (c.text = "");
                b.px && (b = this.canvas.getContext("2d"));
                var d = c.size ? c.size : Math.floor(c.h * c.scale / 100), e = d.toString() + "px " + (c.font ? c.font : "sans-serif");
                c.italic && (e = "italic " + e);
                c.bold && (e = "bold " + e);
                b.font = e;
                b.textBaseline = c.base ? c.base : "middle";
                b.textAlign = c.align ? c.align : "center";
                if (c.clear) {
                    var f = b.measureText(a);
                    b.fillStyle =
                        c.clear;
                    b.fillRect(c.x + c.w / 2 - f.width / 2 - 1, c.y + c.h / 2 - d / 2 - 1, f.width + 2, d + 2)
                }
                b.fillStyle = c.color ? c.color : this.uic.text;
                b.fillText(a, c.x + Math.floor(c.w / 2), c.y + Math.floor(c.h / 2) + 1)
            }
        } catch (h) {
            throw this.exception(h), h;
        }
    };
    this.paintCross = function (a, b) {
        try {
            if (b = this.defaultParams(a, b)) {
                a.px && (a = this.canvas.getContext("2d"));
                b.scale || (b.scale = 75);
                a.strokeStyle = b.color ? b.color : this.uic.cross;
                a.lineWidth = b.width ? b.width : 1;
                var c = b.w * (100 - b.scale) / 200;
                a.beginPath();
                a.moveTo(b.x + c, b.y + c);
                a.lineTo(b.x + b.w - c, b.y + b.h -
                c);
                a.moveTo(b.x + b.w - c, b.y + c);
                a.lineTo(b.x + c, b.y + b.h - c);
                a.stroke()
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintCircle = function (a, b) {
        try {
            if (b = this.defaultParams(a, b)) {
                a.px && (a = this.canvas.getContext("2d"));
                b.scale || (b.scale = 75);
                var c = b.w * b.scale / 200;
                a.strokeStyle = b.stroke ? b.stroke : this.uic.text;
                a.fillStyle = b.fill ? b.fill : this.uic.none;
                a.lineWidth = b.width ? b.width : 2;
                a.beginPath();
                a.arc(b.x + b.w / 2, b.y + b.h / 2, c, 0, 2 * Math.PI);
                a.fillStyle != this.uic.none && a.fill();
                a.strokeStyle != this.uic.none && a.stroke()
            }
        } catch (d) {
            throw this.exception(d),
                d;
        }
    };
    this.paintSquare = function (a, b) {
        try {
            if (b = this.defaultParams(a, b)) {
                a.px && (a = this.canvas.getContext("2d"));
                b.scale || (b.scale = 66);
                var c = b.w * (100 - b.scale) / 200;
                a.strokeStyle = b.stroke ? b.stroke : this.uic.text;
                a.fillStyle = b.fill ? b.fill : this.uic.none;
                a.lineWidth = b.width ? b.width : 2;
                a.beginPath();
                a.rect(b.x + c, b.y + c, b.w - 2 * c, b.h - 2 * c);
                a.fillStyle != this.uic.none && a.fill();
                a.strokeStyle != this.uic.none && a.stroke()
            }
        } catch (d) {
            throw this.exception(d), d;
        }
    };
    this.paintDecagon = function (a, b) {
        try {
            if (b = this.defaultParams(a,
                    b)) {
                a.px && (a = this.canvas.getContext("2d"));
                b.scale || (b.scale = 75);
                var c = [50, 60, 78, 75, 95, 80, 95, 75, 78, 60, 50, 40, 22, 27, 5, 20, 5, 25, 22, 40], d = [5, 22, 15, 32, 35, 50, 65, 65, 85, 75, 95, 75, 85, 65, 65, 50, 35, 32, 15, 22];
                a.strokeStyle = b.stroke ? b.stroke : this.uic.text;
                a.fillStyle = b.fill ? b.fill : this.uic.none;
                a.lineWidth = b.width ? b.width : 1;
                a.beginPath();
                a.moveTo(b.x + c[0] * b.w / 100, b.y + d[0] * b.h / 100);
                for (var e = 1; e < c.length; e++)a.lineTo(b.x + c[e] * b.w / 100, b.y + d[e] * b.h / 100);
                a.lineTo(b.x + c[0] * b.w / 100, b.y + d[0] * b.h / 100);
                a.fillStyle != this.uic.none &&
                a.fill();
                a.strokeStyle != this.uic.none && a.stroke()
            }
        } catch (f) {
            throw this.exception(f), f;
        }
    };
    this.paintDot = function (a, b) {
        try {
            if (b = this.defaultParams(a, b))a.px && (a = this.canvas.getContext("2d")), b.fill = b.color ? b.stroke = b.color : b.stroke = this.uic.black, b.width = 1, b.scale = 10, this.paintSquare(a, b)
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintErrorCircle = function (a, b) {
        try {
            this.paintCircle(a, {stroke: this.uic.error, fill: this.uic.none, scale: b})
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintErrorSquare = function (a,
                                      b) {
        try {
            this.paintSquare(a, {stroke: this.uic.error, fill: this.uic.none, scale: b})
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.paintErrorDot = function (a, b) {
        try {
            this.paintDot(a, {color: this.uic.error, scale: b})
        } catch (c) {
            throw this.exception(c), c;
        }
    };
    this.exception = function (a) {
        if (a && !a.ojdone) {
            a.ojdone = !0;
            a = "Exception: " + a.toString();
            a += "\n\nStack Trace:\n\n";
            for (var b = this.exception, c = 0; b && 10 > c++;)a = b.ojname ? a + (b.ojname + "\n") : b.name ? a + (b.name + "\n") : a + "(unknown)\n", b = b.caller;
            ojdebug(a);
            try {
                a = "Debug Data:\n\n" +
                ojdebugBuffer, a += "\n\n" + this.toString(), a += "\n\nNative Puzzle Data:\n\n" + t, a += "\n\nRaw Puzzle Data:\n" + w
            } catch (d) {
                a = "Exception: this.toString failed"
            }
            try {
                this.server.send(this.server.exception, a)
            } catch (e) {
            }
        }
    }
}
"function" !== typeof Object.getPrototypeOf && (Object.getPrototypeOf = "object" === typeof"test".__proto__ ? function (h) {
    return h.__proto__
} : function (h) {
    return h.constructor.prototype
});
Array.prototype.contains || (Array.prototype.contains = function (h) {
    if (void 0 === this || null === this)throw new TypeError('"this" is null or not defined');
    for (var l = 0; l < this.length; l++)if (this[l] == h)return !0;
    return !1
});
Array.prototype.indexOf || (Array.prototype.indexOf = function (h, l) {
    if (void 0 === this || null === this)throw new TypeError('"this" is null or not defined');
    var p = this.length >>> 0;
    l = +l || 0;
    Infinity === Math.abs(l) && (l = 0);
    0 > l && (l += p, 0 > l && (l = 0));
    for (; l < p; l++)if (this[l] === h)return l;
    return -1
});
Function.prototype.bind || (Function.prototype.bind = function (h) {
    return function (l) {
        var p = this;
        if (1 < arguments.length) {
            var q = h.call(arguments, 1);
            return function () {
                return p.apply(l, arguments.length ? q.concat(h.call(arguments)) : q)
            }
        }
        return function () {
            return arguments.length ? p.apply(l, arguments) : p.call(l)
        }
    }
}(Array.prototype.slice));
String.prototype.contains = function (h) {
    return -1 != this.indexOf(h)
};
String.prototype.startsWith = function (h) {
    return 0 == this.indexOf(h)
};
String.prototype.endsWith = function (h) {
    return -1 != this.indexOf(h, this.length - h.length)
};
String.prototype.replaceAll = function (h, l) {
    return this.replace(RegExp(h, "g"), l)
};
String.prototype.ltrim = function (h) {
    return h ? this.replace(RegExp("^[" + h + "]+"), "") : this.replace(/^\s+/, "")
};
String.prototype.rtrim = function (h) {
    return h ? this.replace(RegExp("[" + h + "]+$"), "") : this.replace(/\s+$/, "")
};
String.prototype.trim = function (h) {
    return h ? this.ltrim(h).rtrim(h) : this.ltrim().rtrim()
};
String.prototype.hash = function () {
    for (var h = 5381, l = 0; l < this.length; l++)var p = this.charCodeAt(l), h = (h << 5) + h + p;
    return h
};
Math.div = function (h, l) {
    return Math.floor(h / l)
};
Math.mod = function (h, l) {
    return h % l
};
Window.prototype.addEvent = function (h, l, p) {
    this.addEventListener ? this.addEventListener(h, l, p) : this.attachEvent ? this.attachEvent("on" + h, l) : this[h] = l
};
Node.prototype.addEvent = Window.prototype.addEvent;
function ojclone(h) {
    if (h instanceof Array)return h.slice(0);
    var l = h.constructor(), p;
    for (p in h)try {
        h.hasOwnProperty(p) && (l[p] = h[p])
    } catch (q) {
    }
    return l
}
function ojpopup(h, l, p) {
    var q = 0;
    l || (l = "ojpuzzle");
    p || (p = document.title);
    document.all && !document.addEventListener && (l = "");
    var s = window.open("", l, "width=" + (400).toString() + ",height=" + (500).toString() + ",top=10,left=" + (screen.width - 400 - 20) + ",resizable=yes,scrollbars=yes,menubar=no,toolbar=no,locationbar=no");
    if (!s)return !1;
    this.init = function (l) {
        var f = l.document;
        f ? (f.close(), f.open(), f.write("<html>\n<head>\n<title>" + p + '</title>\n<meta name="viewport" content="width=device-width, initial-scale=1">\n<meta charset="utf-8">\n</head>\n<body bgcolor=white>\n<pre id="content">\n' +
        h + "</pre>\n</body>\n</html>\n"), f.close(), l.focus()) : (q++, 3 >= q && setTimeout(this.init.bind(this, l), 10))
    };
    this.init(s);
    this.update = function (h) {
        s && s.document && (s.document.getElementById("content").innerHTML = h)
    }
}
var ojassertions = !0, ojdebugging = !1, ojdebugWindow = null, ojdebugBuffer = document.location.href, ojdebugID = "DEBUG";
(function () {
    if (ojdebugBuffer.contains("ojdebug") || ojdebugBuffer.contains("127.0.0.1") || ojdebugBuffer.contains("ojanko.at") || ojdebugBuffer.contains("Usr-pr"))ojdebugging = !0;
    ojdebugging && (ojdebugID = ojdebugBuffer.slice(ojdebugBuffer.lastIndexOf("/") + 1, ojdebugBuffer.lastIndexOf(".")) + "-" + ojdebugID, ojdebugWindow = new ojpopup(ojdebugID, ojdebugID, ojdebugID))
})();
function ojdebug() {
    this.ojname = "g.debug";
    for (var h = "", l = 0; l < arguments.length; l++)h += arguments[l] + " ";
    var p = new Date, l = p.getHours().toString(), q = p.getMinutes().toString(), s = p.getSeconds().toString(), p = p.getMilliseconds().toString();
    1 == l.length && (l = "0" + l);
    1 == q.length && (q = "0" + q);
    1 == s.length && (s = "0" + s);
    2 == p.length && (p = "0" + p);
    1 == p.length && (p = "00" + p);
    h = (l + ":" + q + ":" + s + "." + p + "  " + h).replace(/</g, "&lt;").replace(/>/g, "&gt;");
    ojdebugBuffer = h + "\n" + ojdebugBuffer;
    if (ojdebugging) {
        try {
            ojdebugWindow && ojdebugWindow.update(ojdebugBuffer)
        } catch (v) {
        }
        try {
            console &&
            console.log && console.log(h)
        } catch (f) {
        }
    }
}
function ojassert(h, l) {
    this.ojname = "g.assert";
    if (ojassertions && !h) {
        var p = "", q = ojassert.caller, p = q.ojname ? p + q.ojname : q.name ? p + q.name : p + "(unknown)", p = p + (": " + l);
        ojdebug(p);
        p = Error(p);
        p.name = "Assertion failed";
        throw p;
    }
};
