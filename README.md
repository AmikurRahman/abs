##TITLE OF THE LAB REPORT EXPERIMENT 
Implementation of Modified K-Means Clustering Using Manhattan Distance    with Matrix-Based Visualization in Python


Code :
import random

points = [(random.randint(0, 50), random.randint(0, 50)) for _ in range(100)]

centers = [(random.randint(0, 50), random.randint(0, 50)) for _ in range(10)]

def manhattan_distance(p1, p2):
    return abs(p1[0] - p2[0]) + abs(p1[1] - p2[1])

def assign_clusters(points, centers):
    clusters = {i: [] for i in range(len(centers))}
    for point in points:
        distances = [manhattan_distance(point, center) for center in centers]
        min_index = distances.index(min(distances))
        clusters[min_index].append(point)
    return clusters

def update_centers(clusters):
    new_centers = []
    for points_in_cluster in clusters.values():
        if points_in_cluster:
            avg_x = round(sum(p[0] for p in points_in_cluster) / len(points_in_cluster))
            avg_y = round(sum(p[1] for p in points_in_cluster) / len(points_in_cluster))
            new_centers.append((avg_x, avg_y))
        else:
            new_centers.append((random.randint(0, 50), random.randint(0, 50)))
    return new_centers

for _ in range(10):
    clusters = assign_clusters(points, centers)
    new_centers = update_centers(clusters)
    if new_centers == centers:
        break
    centers = new_centers

grid_size = 51
grid = [['.' for _ in range(grid_size)] for _ in range(grid_size)]

for point in points:
    x, y = point
    grid[y][x] = 'P'

for idx, center in enumerate(centers):
    x, y = center
    grid[y][x] = 'C'

print("\n2D Matrix Visualization:\n")
for row in reversed(grid):
    print(' '.join(row))


