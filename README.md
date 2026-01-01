# growwisepress.com
GrowWisePress Website
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:flutter/foundation.dart'; // For platform detection

void main() {
  runApp(const JigyabooksApp());
}

class JigyabooksApp extends StatelessWidget {
  const JigyabooksApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Jigyabooks',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        // Kid-Friendly Theme: Bright, warm colors and rounded shapes
        primarySwatch: Colors.indigo,
        scaffoldBackgroundColor: const Color(0xFFFDFBF7), // Warm paper color
        fontFamily: 'ComicNeue', // Hypothetical rounded font
        elevatedButtonTheme: ElevatedButtonThemeData(
          style: ElevatedButton.styleFrom(
            backgroundColor: const Color(0xFFFF6B6B), // Bright Coral
            foregroundColor: Colors.white,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(20),
            ),
            padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 12),
            textStyle: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
          ),
        ),
      ),
      home: const HomePage(),
    );
  }
}

// ---------------------------------------------------------------------------
// 1. HOME PAGE: The Library Interface
// ---------------------------------------------------------------------------
class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('🦁 Jigyabooks', style: TextStyle(fontSize: 28)),
        centerTitle: true,
        backgroundColor: Colors.indigo,
        actions:,
      ),
      body: Column(
        children:);
              },
            ),
          ),
        ],
      ),
    );
  }

  void _showSubscriptionDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (context) => const SubscriptionDialog(),
    );
  }
}

// ---------------------------------------------------------------------------
// 2. DISTRIBUTION STRATEGY: The "Download" Logic
// ---------------------------------------------------------------------------
class DownloadBanner extends StatelessWidget {
  const DownloadBanner({super.key});

  @override
  Widget build(BuildContext context) {
    // In a real app, use 'universal_io' or 'kIsWeb' to detect platform accurately.
    // For this prototype, we simulate the logic.
    
    return Container(
      width: double.infinity,
      color: const Color(0xFFFFD166), // Bright Yellow
      padding: const EdgeInsets.all(12),
      child: Column(
        children:,
          ),
        ],
      ),
    );
  }
}

class IOSInstallGuide extends StatelessWidget {
  const IOSInstallGuide({super.key});

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text("Install on iPhone/iPad"),
      content: const Column(
        mainAxisSize: MainAxisSize.min,
        children:,
      ),
      actions:,
    );
  }
}

// ---------------------------------------------------------------------------
// 3. THE READER ENGINE: Karaoke / Read-Along Logic
// ---------------------------------------------------------------------------
class BookReader extends StatefulWidget {
  final Book book;

  const BookReader({super.key, required this.book});

  @override
  State<BookReader> createState() => _BookReaderState();
}

class _BookReaderState extends State<BookReader> {
  int _currentWordIndex = -1;
  bool _isPlaying = false;
  Timer? _syncTimer;
  
  // Simulates the audio playing and syncing
  void _togglePlay() {
    if (_isPlaying) {
      _stop();
    } else {
      _start();
    }
  }

  void _start() {
    setState(() => _isPlaying = true);
    // In a real app, 'audioplayers' stream listener would trigger this update.
    // Here we simulate word progression every 500ms.
    _syncTimer = Timer.periodic(const Duration(milliseconds: 500), (timer) {
      if (_currentWordIndex < widget.book.textSegments.length - 1) {
        setState(() => _currentWordIndex++);
      } else {
        _stop(); // End of page
      }
    });
  }

  void _stop() {
    _syncTimer?.cancel();
    setState(() {
      _isPlaying = false;
      _currentWordIndex = -1; // Reset for demo purposes
    });
  }

  @override
  void dispose() {
    _syncTimer?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text(widget.book.title)),
      body: Column(
        children:,
                image: const DecorationImage(
                  image: NetworkImage("[https://via.placeholder.com/600x400/87CEEB/000000?text=Story+Illustration](https://via.placeholder.com/600x400/87CEEB/000000?text=Story+Illustration)"),
                  fit: BoxFit.cover,
                ),
              ),
              child: Center(
                // Interactive Hotspot Example
                child: GestureDetector(
                  onTap: () {
                     ScaffoldMessenger.of(context).showSnackBar(
                      const SnackBar(content: Text("🔊 Sound Effect: ROAR!")),
                    );
                  },
                  child: Container(
                    padding: const EdgeInsets.all(8),
                    color: Colors.white.withOpacity(0.5),
                    child: const Text("Tap the Lion!", style: TextStyle(fontWeight: FontWeight.bold)),
                  ),
                ),
              ),
            ),
          ),
          
          // Karaoke Text Area
          Expanded(
            flex: 2,
            child: Container(
              padding: const EdgeInsets.symmetric(horizontal: 24),
              child: Center(
                child: RichText(
                  textAlign: TextAlign.center,
                  text: TextSpan(
                    style: const TextStyle(fontSize: 24, color: Colors.black87, height: 1.5, fontFamily: 'ComicNeue'),
                    children: widget.book.textSegments.asMap().entries.map((entry) {
                      int idx = entry.key;
                      String word = entry.value;
                      bool isHighlighted = idx == _currentWordIndex;
                      
                      return TextSpan(
                        text: "$word ",
                        style: isHighlighted
                           ? const TextStyle(color: Colors.red, fontWeight: FontWeight.bold, backgroundColor: Color(0xFFFFE082))
                            : const TextStyle(color: Colors.black87),
                      );
                    }).toList(),
                  ),
                ),
              ),
            ),
          ),

          // Controls
          Container(
            padding: const EdgeInsets.all(24),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children:,
            ),
          ),
        ],
      ),
    );
  }
}

// ---------------------------------------------------------------------------
// 4. DATA MODELS & MOCKS
// ---------------------------------------------------------------------------

class Book {
  final String title;
  final bool isPremium;
  final List<String> textSegments; // Simplified SyncMap for prototype

  Book(this.title, this.isPremium, this.textSegments);
}

// Mock Database (Simulating Strapi CMS Response)
final List<Book> bookDatabase =,
  ),
  Book(
    "Space Adventure",
    true, // Premium Book
   ,
  ),
  Book(
    "The Magic Tree",
    true, // Premium Book
   ,
  ),
];

// ---------------------------------------------------------------------------
// 5. WIDGET COMPONENTS
// ---------------------------------------------------------------------------

class BookCard extends StatelessWidget {
  final Book book;

  const BookCard({super.key, required this.book});

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        if (book.isPremium) {
          // Check subscription status here
          showDialog(context: context, builder: (_) => const SubscriptionDialog());
        } else {
          Navigator.push(context, MaterialPageRoute(builder: (_) => BookReader(book: book)));
        }
      },
      child: Container(
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.circular(16),
          boxShadow:,
        ),
        child: Column(
          children:,
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class SubscriptionDialog extends StatelessWidget {
  const SubscriptionDialog({super.key});

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text("Unlock Jigyabooks Premium"),
      content: Column(
        mainAxisSize: MainAxisSize.min,
        children: const,
      ),
      actions:,
    );
  }
}
