```java
import java.util.*;

class UserSolution
{
    static class Movie {
        int id;
        int genre;
        int totalScore;
        int insertOrder;
        
        Movie(int id, int genre, int totalScore, int insertOrder) {
            this.id = id;
            this.genre = genre;
            this.totalScore = totalScore;
            this.insertOrder = insertOrder;
        }
    }
    
    static class MovieKey implements Comparable<MovieKey> {
        int totalScore;
        int insertOrder;
        
        MovieKey(int totalScore, int insertOrder) {
            this.totalScore = totalScore;
            this.insertOrder = insertOrder;
        }
        
        @Override
        public int compareTo(MovieKey other) {
            // 총점이 높은 순, 같으면 최신 등록순
            if (this.totalScore != other.totalScore) {
                return Integer.compare(other.totalScore, this.totalScore);
            }
            return Integer.compare(other.insertOrder, this.insertOrder);
        }
    }
    
    static class WatchedMovie implements Comparable<WatchedMovie> {
        int movieId;
        int rating;
        int watchOrder;
        
        WatchedMovie(int movieId, int rating, int watchOrder) {
            this.movieId = movieId;
            this.rating = rating;
            this.watchOrder = watchOrder;
        }
        
        @Override
        public int compareTo(WatchedMovie other) {
            // 사용자가 준 평점이 높은 순, 같으면 최근 시청순
            if (this.rating != other.rating) {
                return Integer.compare(other.rating, this.rating);
            }
            return Integer.compare(other.watchOrder, this.watchOrder);
        }
    }
    
    static Map<Integer, Movie> allMovies; // 모든 영화 정보
    static TreeMap<MovieKey, Integer> moviesByScore; // 총점 기준 정렬된 영화들
    static Map<Integer, TreeMap<MovieKey, Integer>> moviesByGenre; // 장르별 영화들
    static Map<Integer, List<WatchedMovie>> userWatchHistory; // 사용자별 시청 기록 (시청 순서)
    static Map<Integer, Set<Integer>> userWatchedMovies; // 사용자가 본 영화 ID들
    
    static int movieInsertOrder;
    static int watchOrder;
    
    void init(int N) {
        allMovies = new HashMap<>();
        moviesByScore = new TreeMap<>();
        moviesByGenre = new HashMap<>();
        userWatchHistory = new HashMap<>();
        userWatchedMovies = new HashMap<>();
        
        movieInsertOrder = 0;
        watchOrder = 0;
        
        //초기화
        for (int i = 1; i <= N; i++) {
            userWatchHistory.put(i, new ArrayList<>());
            userWatchedMovies.put(i, new HashSet<>());
        }
    }
    
    int add(int mID, int mGenre, int mTotal) {
        if (allMovies.containsKey(mID)) {
            return 0; // 이미 존재
        }
        
        Movie movie = new Movie(mID, mGenre, mTotal, movieInsertOrder++);
        allMovies.put(mID, movie);
        
        MovieKey key = new MovieKey(mTotal, movie.insertOrder);
        moviesByScore.put(key, mID);
        
        moviesByGenre.computeIfAbsent(mGenre, k -> new TreeMap<>()).put(key, mID);
        
        return 1;
    }
    
    int erase(int mID) {
        Movie movie = allMovies.get(mID);
        if (movie == null) {
            return 0; // 존재x
        }
        
        // 전체 영화 목록에서 제거
        MovieKey key = new MovieKey(movie.totalScore, movie.insertOrder);
        moviesByScore.remove(key);
        moviesByGenre.get(movie.genre).remove(key);
        allMovies.remove(mID);
        
        // 모든 사용자의 시청 기록에서 제거
        for (List<WatchedMovie> watchHistory : userWatchHistory.values()) {
            watchHistory.removeIf(watched -> watched.movieId == mID);
        }
        for (Set<Integer> watchedSet : userWatchedMovies.values()) {
            watchedSet.remove(mID);
        }
        
        return 1;
    }
    
    int watch(int uID, int mID, int mRating) {
        Movie movie = allMovies.get(mID);
        if (movie == null) {
            return 0; // 존재x
        }
        
        if (userWatchedMovies.get(uID).contains(mID)) {
            return 0; // 이미 시청
        }
        
        // 영화 총점 업데이트
        MovieKey oldKey = new MovieKey(movie.totalScore, movie.insertOrder);
        moviesByScore.remove(oldKey);
        moviesByGenre.get(movie.genre).remove(oldKey);
        
        movie.totalScore += mRating;
        
        MovieKey newKey = new MovieKey(movie.totalScore, movie.insertOrder);
        moviesByScore.put(newKey, mID);
        moviesByGenre.get(movie.genre).put(newKey, mID);
        
        // 사용자 시청 기록 추가
        userWatchHistory.get(uID).add(new WatchedMovie(mID, mRating, watchOrder++));
        userWatchedMovies.get(uID).add(mID);
        
        return 1;
    }
    
    Solution.RESULT suggest(int uID) {
        Solution.RESULT result = new Solution.RESULT();
        result.cnt = 0;
        
        List<WatchedMovie> watchHistory = userWatchHistory.get(uID);
        Set<Integer> watchedMovies = userWatchedMovies.get(uID);
        
        int targetGenre = -1;
        
        if (!watchHistory.isEmpty()) {
            // 최근 5개 영화
            List<WatchedMovie> recentMovies = new ArrayList<>();
            for (int i = Math.max(0, watchHistory.size() - 5); i < watchHistory.size(); i++) {
                recentMovies.add(watchHistory.get(i));
            }
            
            // 최근 5개를 정렬
            recentMovies.sort((a, b) -> {
                if (a.rating != b.rating) {
                    return Integer.compare(b.rating, a.rating); // 평점 높은순
                }
                return Integer.compare(b.watchOrder, a.watchOrder); // 최근순
            });
            
            // 가장 높은 평점
            WatchedMovie bestMovie = recentMovies.get(0);
            Movie movie = allMovies.get(bestMovie.movieId);
            if (movie != null) {
                targetGenre = movie.genre;
            }
        }
        
        // 추천할 영화들
        TreeMap<MovieKey, Integer> candidateMovies;
        if (targetGenre == -1) {
            // 시청 기록이 없음
            candidateMovies = moviesByScore;
        } else {
            candidateMovies = moviesByGenre.getOrDefault(targetGenre, new TreeMap<>());
        }
        
        // 이미 시청한 영화 제외하고 추천
        for (int movieId : candidateMovies.values()) {
            if (!watchedMovies.contains(movieId)) {
                result.IDs[result.cnt++] = movieId;
                if (result.cnt == 5) break;
            }
        }
        
        return result;
    }
}
```
