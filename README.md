<h1>Go Generics</h1>
<p>Go generics is the feature that allows you to pass a parameter to function within multi types of variable by the example below</p>

<p>I have a type of Movie and Game that are similar together just different in Platform field. But I need to find an average for each type how I can do this?</p>

```go
type GameOrMovie interface {
	getPrice() float64
}

type Game struct {
	Title    string
	Price    float64
	Platform string
}

type Movie struct {
	Title string
	Price float64
}
```

<br>
<p>If <strong>Go Generics</strong> doesn't exist I'm going to do like this below one</p>

```go
func AverageGamePrice(obj []Game) float64 {
	var result float64
	for i := range obj {
		result += obj[i].Price
	}
	return result / float64(len(obj))
}
func AverageMoviePrice(obj []Movie) float64 {
	var result float64
	for i := range obj {
		result += obj[i].Price
	}
	return result / float64(len(obj))
}

func main() {
	games := []Game{
		{
			Title:    "MINECRAFT",
			Price:    29.99,
			Platform: "PC",
		},
		{
			Title:    "FALLOUT 4",
			Price:    10.99,
			Platform: "PC",
		},
		{
			Title:    "NO MAN'S SKY",
			Price:    19.99,
			Platform: "PC",
		},
	}

	movies := []Movie{
		{
			Title: "Hello World",
			Price: 5.99,
		},
		{
			Title: "Death Note",
			Price: 6.99,
		},
		{
			Title: "Forrest Gump",
			Price: 7.99,
		},
	}

	// Calculate an average value for each object
	fmt.Printf("games: %.2f\n", AverageGamePrice(games))
	fmt.Printf("movies: %.2f\n", AverageMoviePrice(movies))
}
```

<p>Output</p>

```bash
games: 20.32
movies: 6.99
```

<br>
<p>Now, let's apply an <strong>Go Generics</strong> to our code</p>

```go
// Implement a method for each object
func (obj Game) getPrice() float64 {
	return obj.Price
}
func (obj Movie) getPrice() float64 {
	return obj.Price
}

// Method
func Average[V GameOrMovie](obj []V) float64 {
	var result float64
	for i := range obj {
		result += obj[i].getPrice()
	}
	return result / float64(len(obj))
}

func main() {
	games := []Game{
		{
			Title:    "MINECRAFT",
			Price:    29.99,
			Platform: "PC",
		},
		{
			Title:    "FALLOUT 4",
			Price:    10.99,
			Platform: "PC",
		},
		{
			Title:    "NO MAN'S SKY",
			Price:    19.99,
			Platform: "PC",
		},
	}

	movies := []Movie{
		{
			Title: "Hello World",
			Price: 5.99,
		},
		{
			Title: "Death Note",
			Price: 6.99,
		},
		{
			Title: "Forrest Gump",
			Price: 7.99,
		},
	}

	// Calculate an average value for each object
	fmt.Printf("games: %.2f\n", Average(games))
	fmt.Printf("movies: %.2f\n", Average(movies))
}
```

<p>Output</p>

```bash
games: 20.32
movies: 6.99
```

<p>Ahhhhh... look better now. and all results are the same</p>