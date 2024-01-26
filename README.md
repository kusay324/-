#include <httplib.h>
#include <iostream>

class QuranServer {
public:
    QuranServer() {
        svr.Get("/", [this](const httplib::Request& req, httplib::Response& res) {
            handleRequest(req, res);
        });

        std::cout << "Server is running on http://localhost:8080" << std::endl;
        svr.listen("localhost", 8080);
    }

private:
    void handleRequest(const httplib::Request& req, httplib::Response& res) {
        std::string html = "<html><body><h1>تطبيق القرآن الكريم - الصفحة الرئيسية</h1>";
        html += "<p>مرحبًا بك في تطبيق القرآن الكريم. لاستخدام الخادم، افتح المتصفح وانتقل إلى <a href='/app'>/app</a>.</p>";
        html += "</body></html>";

        res.set_content(html, "text/html");
    }

    httplib::Server svr;
};

int main() {
    QuranServer server;
    return 0;
}
